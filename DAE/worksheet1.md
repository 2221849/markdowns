# Enterprise Application Development

## Worksheet 1

### Installation

#### Install Chocolatey

- Run PowerShell as Administrator and execute the following command to install Chocolatey:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

#### Install necessary software using Chocolatey

```powershell
choco install docker-desktop temurin17 maven make
```

#### Install IntelliJ IDEA Ultimate

- Download and install the latest version of [IntelliJ IDEA Ultimate](https://www.jetbrains.com/idea/download/).

### Project Setup

1. **Create a new project in IntelliJ IDEA Ultimate**:
   - Click "New Project".
   - Configure the following:
     - **Name**: academics
     - **Location**: Choose a location
     - **Project template**: REST Service
     - **Application Server**: Leave empty (we will use Wildfly in a container)
     - **Language**: Java
     - **Build system**: Maven
     - **Group**: `pt.ipleiria.estg.dei.ei.dae`
     - **Artifact**: academics
     - **Project SDK**: temurin-17
   - Click “Next”.
   - Select:
     - **Version**: Jakarta EE 9.1
     - **Dependencies → Specifications**: Web Profile (will select a bundle of options).
     - **Dependencies → Implementations**: Hibernate and Hibernate Validator.
   - Click "Create".

2. **Modify project configuration**:
   - In the `pom.xml` file, replace this section:

   ```xml
   <plugin>
     <groupId>org.apache.maven.plugins</groupId>
     <artifactId>maven-war-plugin</artifactId>
     <version>3.3.2</version>
   </plugin>
   ```

   - With this:

   ```xml
   <plugin>
     <groupId>org.apache.maven.plugins</groupId>
     <artifactId>maven-war-plugin</artifactId>
     <version>3.3.2</version>
     <configuration>
       <outputDirectory>target</outputDirectory>
       <warName>academics</warName>
     </configuration>
   </plugin>
   ```

3. **Move Docker files**:
   - Move the files from `docker-wildfly-postgres-main` to the project root directory.

4. **Configure Persistence**:
   - Open the `persistence.xml` file in `src/main/resources/META-INF` and replace the `<persistence-unit/>` tag with:

   ```xml
   <persistence-unit name="AcademicsPersistenceUnit" transaction-type="JTA">
       <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
       <jta-data-source>java:/AcademicsDS</jta-data-source>
       <properties>
           <property name="jakarta.persistence.schema-generation.database.action" value="drop-and-create" />
       </properties>
   </persistence-unit>
   ```

5. **Start Docker Containers**:
   - Ensure **Docker Engine** is running before executing any `make` commands.
   - Open a terminal in the project root and run the following command with Docker running:

   ```sh
   make up
   ```

   You can check container status anytime with `make up`. Access the application at [localhost:8080](http://localhost:8080). You can also check the Wildfly Admin Console at [localhost:9990](http://localhost:9990).

6. **Test the database**:
   - Go to "Configuration → Subsystems → Datasources & Drivers → Datasources → AcademicsDS".
   - Click “Test connection” to ensure it’s working.

### Developing the Application

1. **Modify Jakarta EE version**:
   - Ensure the Jakarta EE version in the `pom.xml` is set to 9.1.0.

2. **Create EJB**:
   - Create a package: `pt.ipleiria.estg.dei.ei.dae.academics.ejbs`.
   - Create a singleton EJB named `ConfigBean` with the following code:

   ```java
   package pt.ipleiria.estg.dei.ei.dae.academics.ejbs;
   import jakarta.annotation.PostConstruct;
   import jakarta.ejb.Singleton;
   import jakarta.ejb.Startup;

   @Startup
   @Singleton
   public class ConfigBean {
       @PostConstruct
       public void populateDB() {
           System.out.println("Hello Java EE!");
       }
   }
   ```

3. **Deploy the application**:
   - Run this command to deploy:

   ```sh
   make deploy
   ```

4. **Create the Student entity**:
   - Create the `Student` entity in `pt.ipleiria.estg.dei.ei.dae.academics.entities` with attributes:
     - `username` (as the entity ID),
     - `password`, `name`, and `email`.
   - Example:

   ```java
   @Entity
   public class Student {
       @Id
       private String username;
       private String password;
       private String name;
       private String email;
       // Constructors, getters, setters
   }
   ```

5. **Create StudentBean EJB**:
   - In the `ejbs` package, create the `StudentBean` EJB to persist students:

   ```java
   @Stateless
   public class StudentBean {
       @PersistenceContext
       private EntityManager entityManager;

       public void create(String username, String password, String name, String email) {
           var student = new Student(username, password, name, email);
           entityManager.persist(student);
       }
   }
   ```

6. **Update ConfigBean**:
   - Modify `ConfigBean` to use `StudentBean` to create and persist a student:

   ```java
   public class ConfigBean {
       @EJB
       private StudentBean studentBean;

       @PostConstruct
       public void populateDB() {
           studentBean.create("user1", "pass", "Student Name", "email@example.com");
       }
   }
   ```

7. **Check database contents**:
   - Run the following to check the data:

   ```sh
   make sql
   ```

   Use SQL commands to verify the student records, like `SELECT * FROM student`.

8. **View database in IntelliJ**:
   - Configure the datasource in IntelliJ:
     - Name: academics
     - User: postgres
     - Password: dbsecret
     - Database: academics
     - URL: `jdbc:postgresql://localhost:5432/academics`
     - Click "Test Connection".
     - **If the “Download missing drivers” link is available**, click on it to download the necessary drivers.

   - View tables by expanding the datasource and refreshing.

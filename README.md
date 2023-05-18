# SpringBootDocumentation
Documentation Spring  Boot

Dependencias
Lombok
OracleDriver
Spring Devtools
JPA
Spring Web
Thymeleaf


## Paso 1
application.properties:

server.port=8081

spring.datasource.url=jdbc:oracle:thin:@//localhost:1521/XEPDB1
spring.datasource.username=sys as sysdba
spring.datasource.password=admDa1gjMWtp

spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=none



## Paso 2 Crear Paquetes

Paso 1 Crear Entity con la clase Modelo con la anotacion @Entity, @Table(name="") y @Id en el id opcional @GenerateValue(strategy = GenerationType.AUTO) y su constructor y getters y setters

Paso 2 Crear Repository con la Interface TablaRepository extends JpaRepository<Clase, IDType> y con la Anotacion @Repository

Paso 3 Crear Controller, con la anotacion  @Controller y @AutoWired ReposiClass repository

en templates de src/main/resources
crear los .html, 
los html  se retornan en los enlaces del controller home.html = return "home"
luego buscar en bootstrap
buscar Starter Template
a la par de xmlns:th="https://www.thymeleaf.org"
para el ejemplo de Motrar Datos

debemos copiar la tabla simple de Bootstrap

en un div clas= container
en el thead = 
en el tbody = en el tr th:each="student: ${studentlist}", en el th y td th:text="${student.id y demas} para listar

en el metodo que se envia la data Model model, model.addAttribute("studentlist",repo.findAll());


##Oracle

DECLARE
num1 number;
num2 number;
result number;

BEGIN
num1:= 5;
num2:= 10;
result:=num1+num2;

dbms_output.put_line("El resultado es:" || result);
END;




##Query personalizado


public interface TuRepositorio extends JpaRepository<EntidadA, Long> {

    @Query("SELECT a FROM EntidadA a INNER JOIN a.entidadB b WHERE b.algunCampo = :valor")
    List<EntidadA> encontrarPorCampoDeEntidadB(@Param("valor") String valor);

}




##HTML LOGIN
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Login</title>
</head>
<body>
    <h2>Login</h2>
    <form action="#" th:action="@{/login}" method="post">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required>
        <br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required>
        <br>
        <input type="submit" value="Login">
    </form>
</body>
</html>


@GetMapping("/")
    public String redirectToLogin() {
        return "redirect:/login";
    }

@GetMapping("/login")
    public String showLoginPage() {
        return "login";
    }

    @PostMapping("/login")
    public String login(@RequestParam("username") String username, @RequestParam("password") String password, Model model) {
        User user = userRepository.findByUsername(username);
        if (user != null && user.getPassword().equals(password)) {
            // Usuario válido, puedes realizar alguna acción o redireccionar a otra página
            return "redirect:/dashboard";
        } else {
            model.addAttribute("error", "Invalid username or password");
            return "login";
        }
    }

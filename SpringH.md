![image](https://github.com/SpringBootJav/SpringBootDocumentation/assets/133820804/811ebd11-04ca-4d20-b4d4-4c7d0fca3ef8)

```
<!doctype html>
<html lang="en" xmlns:th="https://www.thymeleaf.org">
  <head>

    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.rtl.min.css" integrity="sha384-T5m5WERuXcjgzF8DAb7tRkByEZQGcpraRTinjpywg37AO96WoYN9+hrhDVoM6CaT" crossorigin="anonymous">

    <title>Home Page</title>
  </head>
  <body>
    
  
  <div class="container"><br>
  <a th:href="@{/saveStudentPage}" class="btn btn-primary">Create User</a>
  <table class="table">
  <thead>
    <tr>
      <th scope="col">StudentId</th>
      <th scope="col">StudentName</th>
      <th scope="col">StudentAddress</th>
      <th scope="col">Email</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody >
    <tr th:each="student: ${studentlist}">
      <th th:text="${student.id}" scope="row"></th>
      <td th:text="${student.name}" ></td>
      <td th:text="${student.address}" ></td>
      <td th:text="${student.email}" ></td>
      <td>
      <a th:href="@{/updateStudentPage/{id}(id=${student.id})}" class="btn btn-primary">Update</a>
      <a th:href="@{/deleteStudent/{id}(id=${student.id})}" class="btn btn-danger">Delete</a>
      </td>
    </tr>
    
  </tbody>
</table>

  </div>
  </body>
</html>
```
	@GetMapping("/saveStudentPage")
	public String saveStudentPage(Model model) {
		Student student=new Student();
		model.addAttribute("student", student);
		return "add_student";
	}
	
	@PostMapping("/saveStudent")
	public String saveStudent(@ModelAttribute("student") Student student) {
		repo.save(student);
		return "redirect:/";
	}

## Update

```
<!doctype html>
<html lang="en" xmlns:th="https://www.thymeleaf.org">
  <head>

    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.rtl.min.css"  >

    <title>Update Page</title>
  </head>
  <body>
    

  <div class="container"><br>
  <h1 style="color:red">Student Update Form</h1>
  <form action="" class="col-5" th:action="@{/saveStudent}" th:object="${student}" method="post">
  
  <div class="mb-3">
  <label for="exampleFormControlInput1" class="form-label">StudentId</label>
  <input type="text" th:field="*{id}" class="form-control">
</div>

<div class="mb-3">
  <label for="exampleFormControlInput1" class="form-label">StudentName</label>
  <input type="text" th:field="*{name}" class="form-control">
</div>

<div class="mb-3">
  <label for="exampleFormControlInput1" class="form-label">StudentAddress</label>
  <input type="text" th:field="*{address}" class="form-control">
</div>

<div class="mb-3">
  <label for="exampleFormControlInput1" class="form-label">Email</label>
  <input type="email" th:field="*{email}" class="form-control">
</div>
<button type="submit" class="btn btn-success">Update Student</button>
<br>
</form>
<br>
  <a th:href="@{/}" >HomePage</a>
  
  </div>
  </body>
</html>
```
    @GetMapping("/updateStudentPage/{id}")
	public String showUpdateStudentPage(@PathVariable("id") int id, Model model) {
		java.util.Optional<Student> temp = repo.findById(id);
		Student student = (Student) temp.get();
		model.addAttribute("student", student);
		return "update_student";
	}

![image](https://github.com/SpringBootJav/SpringBootDocumentation/assets/133820804/5e20d126-ff1a-4245-810d-a27bb0a5b7af)

	@Autowired
	private StudentRepo repo;
	
	@GetMapping("/")
	public String homePage(Model model) {
		model.addAttribute("studentlist", repo.findAll());
		return "home";
	}
	
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
	
	@GetMapping("/updateStudentPage/{id}")
	public String showUpdateStudentPage(@PathVariable("id") int id, Model model) {
		java.util.Optional<Student> temp = repo.findById(id);
		Student student = (Student) temp.get();
		model.addAttribute("student", student);
		return "update_student";
	}
	
	@GetMapping("/deleteStudent/{id}")
	public String deleteStudent(@PathVariable("id") int id) {
		repo.deleteById(id);
		return "redirect:/";
	}

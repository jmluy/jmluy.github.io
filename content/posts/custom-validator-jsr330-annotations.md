+++ 
title = "Using a custom validator with JSR 303 annotations"
draft = true
date = 2010-09-28T09:16:22+08:00
description = ""
slug = "custom-validator-jsr330-annotations" 
tags = ["spring mvc"]
categories = ["development", "spring mvc"]
externalLink = ""
series = []
+++

I was using JSR 303 annotations for validating my models but i had a scenario where i need to extend the validation by adding my own validator. So what i did was create a validator implementing spring's validator interface then extending LocalValidatorFactoryBean. The thing to note is not to instantiate the validator yourself but just add the autowire annotation and let the container inject the correct validator for you.

The model
```
public class User {
   @NotEmpty
   @Size(min=3, max=20)
   private String userName

   @NotEmpty
   @Size(min=1, max=30)
   private String firstName;

   @NotEmpty
   @Size(min=1, max=30)
   private String lastName;
}
```

A snippet of the controller
```
@Autowired
private Validator userValidator;

@InitBinder
protected void initBinder(WebDataBinder binder) {
   binder.setValidator(userValidator);
}

@RequestMapping(value="/create", method = RequestMethod.POST)
public String add(@Valid User user, BindingResult result) {
    if (result.hasErrors()) {
        return "/admin/createUser";
    }
    
    this.users.put(user.getUserName(), user);
    return "redirect:/admin/listUsers";
}
```

The custom validator
```
@Component
public class UserValidator extends LocalValidatorFactoryBean implements Validator { 
    @Override
    public boolean supports(Class clazz) {
        return User.class.isAssignableFrom(clazz);
    }

    @Override
    public void validate(Object target, Errors errors) {
        super.validate(target, errors);
        User user = (User) target;
        if (user != null) {
            // custom validation here
        }
    }
}
```
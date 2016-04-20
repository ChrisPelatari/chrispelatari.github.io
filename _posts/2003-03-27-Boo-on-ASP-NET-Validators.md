---
layout: post
title: Boo! on ASP.NET Validators!
---
So I'm trying to get a regular expression validator to 
work - ya know, validate my data. I'm a reeeeal novice when it comes to regex, 
so with a little help and tweaking, this is what I come up with:

`ValidationExpression = "(\d{1,8}(\.\d{1,2})?)|(\d{0,8}(\.\d{1,2}))|(N\/A)"`

Because I want a decimal number OR N/A, which is the default value that each of my textboxes (in this case) are populated with. This regular expression works. Almost. I could *not* figure out why I could add an empty string or a bunch of spaces and it validates as true. So I took a look at the WebUIValidation.js that the validators use.

`function RegularExpressionValidatorEvaluateIsValid(val) {
  var value = ValidatorGetValue(val.controltovalidate);  
  if (ValidatorTrim(value).length == 0)    
    return true;     
  var rx = new RegExp(val.validationexpression);    
  var matches = rx.exec(value);    
  return (matches != null && value == matches[0]);  
}`
  
The important bit is the if(ValidatorTrim) part. It's valid if there is nothing there! Maybe I'm just dense...wait...it's *probably* because I'm dense, but I want my regular expression validator to match my regular expression *only*. I know I could add a required field validator, but that is not correct. It's *not* a required field - that's why N/A is a valid value. But a space/no entry is not. I want the value in my field to be :

a decimal number OR "N/A" ONLY!

grrrrrrr...I don't know if I should modify the WebUIValidation.js or write my own control that will strictly match a Regular Expression. Sucks on empty strings.
## Template driven forms -> 

1. events in () 
2. local reference variable -> `#myForm`, #myform="ngForm" -> so NgForm object in myForm variable
3. form as DOM Object will show whole html element, but we can also get it as typescript object. SO we can get object of type `NgForm`
4. object of type ngForm have `controls property`
5. `ngModel` -> tells angular that this input element is control of this form
6. `NgForm` object also have values property
7. `dirty` property in form becomes true when something in form changes, when we type something
8. `at view child decorator`
9. we define `validation` in html

## Template driven form validation -> 

1. `property binding` -> [name]="myName"
2. `class1.class2` -> both classes should be there on element
3. `two way data binding` -> [(ngModel)]="username", achieved through ngModel directive, which is combination of property binding and event binding

## Form control group in template driven form - >

1.  we can group firstname, lastname, email form controls together. For this we will create a container and on that container we will add `ngModelGroup`
2. angular adds some `css classes` on each of the form controls

## Radio button in template driven form -> 

1. loop the array with html template 

## setValue and patchValue in Template driven form ->

1. to update the values of form controls
2. `setValue()` -> to set some value for form control. The object we pass to setValue() must match the structure of the value object in `ngForm object`
3. If we do not want to set the value for all the form controls -> `patchValue()`
4. in `patchValue()` -> specify the structure of object we want to update
5. `patchValue()` -> when we want to update a subset of form controls of ngForm or formGroup

## retrieving FormData and resetting form -> 

1. in two way data binding -> value shown as soon as we entered , not waited for submit to be clicked
2. `reading the ngForm object properties` and assigning to properties of app.component class
3. `reset() method on ngForm object`, this makes form controls empty as well as resets the form state`(original css classes will be added again)`

-----------------------------------------------------------------------------------------------------------------------

## Reactive forms -> 

1. we define logic and controls in the html template itself
2. template driven form -> `FormsModule`, reactive form -> `ReactiveFormsModule`
3. `OnInit` -> interface
4. `formGroup`, `formControlName`

## Form validation of reactive form -> 

1. in `reactive forms` we create form in class and then synchronise form with html
1. by default form is valid 
2. in template driven forms we used some angular directives like required, email etc on html itself
3. in reactive form we will add validation in typescript class
4. fields should store a valid value
5. `Validators` from angular doc
6. `[Validators.required, Validators.email]`
7. custom validation error message -> `reactiveForm.get('email').valid`. If we sub-grouped email into a seperate formGroup then we will write : `reactiveForm.get('personDetails.email').valid`

## Group Form Control in Reactive Form -> 

1. `formGroupName` directive -> to group form controls together in a reactive form

## Form Array in reactive form - >

1. `FormArray` is a way to manage collection fo form controls. The controls can be `FormGroup, FormControl or another FormArray`
2. for this also we will create a contianer div
3. `formArrayName` directive
4. `skills : new FormArray([a,b,c])`, 
5. in the starting formArray input elements will not have any state because they are not binded to angular form. They will be binded to anglar form when we use `formControlName directive`
6. in `this.reactiveForm.get('skills')` we need to explicitly typecast the value which this get method will return because get method can return any value, so we will do -> `(<FormArray>this.reactiveForm.get('skills')).push(new FormControl(null))`. WIth this we can `add form control dynamically to a form`
7. So using `formArray` we can generate form controls dynamically , add validations on them 

## Custom Validation and error codes in reactive forms -> 
 
1. every validator has an error code. SO required is the error code for required validator
2. so every validator returns an error code when validation fails on a form control and we can see that error code in errors object of the form control
3. validator is nothing but a method, like `required()`
4. We can also use error codes in our app for displaying dynamic error messages
5. `handle null reference` -> nullish coelecing operator
6. so based on the error code returned by the validator, which is stored in the errors object of the form control, we are displaying a custom validation error message

## Custom Async validator in reactive forms -> 

1. async validator must return a promise or observable
2. angular does not provide any built in async validator
3. when we send http request to server to check if data is valid
4. `validator is just a function`. SO on whichever formcontrol we use validator, we will receive that form control as an argument and it will be stored inside control parameter we supply to validator method
5. required, email -> `sync validators` -> we pass as 2nd argument in form control constructor
6. `async validator` -> we pass as 3rd argument in form control constructor
7. for this, angular addds `ng-pending` css class on control

## Value and Status change events -> 

1. `value changes` -> event by angular forms when value of FormControl, FormGroup or FormArray changes. `value changes` event returns an observable so we can subscribe to it
2. `status change` -> every form control has a status, either that form control will be valid, invalid or pending
3. if any form control is invalid, then wholw form group is invalid
4. `status change` -> event by angular forms when angular calculates validation status of a FormControl, FormGroup or FormArray
5. `[ngClass] directive` -> conditionally apply css classes
6. for basic css, just apply css directly. For basic components like model, pop up, accordian use angular material

## setValue() and patchValue() in reactive forms -> 

1. same as template driven form
2. this.reactiveForm.patchValue()
2. `this.reactiveForm.reset()` -> reset a reactive form, will also reset the status of each of these form controls. `reset()` can also take an object
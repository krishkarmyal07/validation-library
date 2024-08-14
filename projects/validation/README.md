
This library was generated with [Angular CLI](https://github.com/angular/angular-cli) version 16.2.0.

# Validation Library

An Angular library for form validation including email validation, password strength validation, and password confirmation matching.

## Installation

To install the library, use npm:

```bash
npm install ng-confirm-password-validator --save 
```



## Usage

Using the Validators
Create a form in your component and use the validators provided by the library:

```typescript
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { emailValidator, passwordStrengthValidator, passwordMatchValidator } from 'ng-confirm-password-validator'; // Import validators

@Component({
  selector: 'app-user-form',
  templateUrl: './user-form.component.html'
})
export class UserFormComponent {
  form: FormGroup;

  constructor(private fb: FormBuilder) {
    this.form = this.fb.group(
      {
        email: ['', [Validators.required, emailValidator()]],
        password: ['', [Validators.required, passwordStrengthValidator()]],
        confirmPassword: ['', [Validators.required]],
      },
      { validators: passwordMatchValidator('password', 'confirmPassword') }
    );
  }

  onSubmit() {
    if (this.form.valid) {
      console.log('Form Submitted', this.form.value);
    }
  }
}
```
Form Template Example
Here’s an example of how to create the form template with validation feedback:

```html
<form [formGroup]="form" (ngSubmit)="onSubmit()">

    <label for="email">Email:</label>
    <input id="email" formControlName="email" type="text" />
    <div *ngIf="form.controls['email'].invalid && form.controls['email'].touched">
        <div *ngIf="form.controls['email'].errors?.['required']">Email is required.</div>
        <div *ngIf="form.controls['email'].errors?.['invalidEmail']">Invalid email format.</div>
    </div>

    <label for="password">Password:</label>
    <input id="password" formControlName="password" type="password" />
    <div *ngIf="form.controls['password'].invalid && form.controls['password'].touched">
        <div *ngIf="form.controls['password'].errors?.['required']">Password is required.</div>
        <div *ngIf="form.controls['password'].errors?.['passwordStrength']">Password must include uppercase, lowercase,
            numeric, and special characters.</div>
    </div>

    <label for="confirmPassword">Confirm Password:</label>
    <input id="confirmPassword" formControlName="confirmPassword" type="password" />
    <div *ngIf="form.errors?.['passwordMismatch'] && form.controls['confirmPassword'].touched">
        <div>Passwords do not match.</div>
    </div>

    <button type="submit" [disabled]="form.invalid">Submit</button>

</form>
```

Running the Application
After setting up the form, start your Angular application to test the validators:

## Contributing

Pull requests are welcome.


### Submitted by

[Krishna Karmyal](https://www.linkedin.com/in/krishna-karmyal/)

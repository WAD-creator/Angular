# Angular
# Angular Authentication App Setup

## Step 1: Install Angular CLI and Create Project

Open your terminal and run the following commands:

**1. Install Angular CLI globally**
```bash
npm install -g @angular/cli
```

**2. Create a new Angular project named `ass3`**
```bash
ng new ass3
```

**3. Navigate into your project folder**
```bash
cd ass3
```

**4. Generate components (Register, Login, Profile)**
```bash
ng generate component register
ng generate component login
ng generate component profile
```

---

## Step 2: Configure Routing
Open `src/app/app.routes.ts` and replace its contents with:

```typescript
import { Routes } from '@angular/router';

import { RegisterComponent } from './register/register';
import { LoginComponent } from './login/login';
import { ProfileComponent } from './profile/profile';

export const routes: Routes = [
  { path: '', component: RegisterComponent },
  { path: 'login', component: LoginComponent },
  { path: 'profile', component: ProfileComponent }
];
```

---

## Step 3: Configure the Root Application Component
**1. Open `src/app/app.html`** and replace the content with:
```html
<h1 align="center">User Management App</h1>

<div align="center">
  <a routerLink="">Register</a> |
  <a routerLink="/login">Login</a> |
  <a routerLink="/profile">Profile</a>
</div>

<hr>

<router-outlet></router-outlet>
```

**2. Open `src/app/app.ts`** and replace the content with:
```typescript
import { Component } from '@angular/core';
import { RouterOutlet, RouterLink } from '@angular/router';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    RouterOutlet,
    RouterLink
  ],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {

}
```
## Step: Configure the Root Application Component
**1. Open `src/app/app.config.ts`** and replace the content with:
```typescript
import { ApplicationConfig } from '@angular/core';
import { provideRouter } from '@angular/router';

import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes)
  ]
};
```

---

## Step 4: Register Component
**1. Open `src/app/register/register.ts`** and replace the content with:
```typescript
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-register',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './register.html',
  styleUrl: './register.css'
})
export class RegisterComponent {

  user = {
    name: '',
    email: '',
    password: ''
  };

  registerUser() {

    localStorage.setItem(
      'user',
      JSON.stringify(this.user)
    );

    alert('User Registered Successfully');
  }
}
```

**2. Open `src/app/register/register.html`** and replace the content with:
```html
<h2>Register User</h2>

Name:
<input type="text" [(ngModel)]="user.name">
<br><br>

Email:
<input type="email" [(ngModel)]="user.email">
<br><br>

Password:
<input type="password" [(ngModel)]="user.password">
<br><br>

<button (click)="registerUser()">
  Register
</button>
```

---

## Step 5: Login Component
**1. Open `src/app/login/login.ts`** and replace the content with:
```typescript
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { Router } from '@angular/router';

@Component({
  selector: 'app-login',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './login.html',
  styleUrl: './login.css'
})
export class LoginComponent {

  email = '';
  password = '';

  constructor(private router: Router) {}

  loginUser() {

    let data: any =
      localStorage.getItem('user');

    let user = JSON.parse(data);

    if (
      this.email == user.email &&
      this.password == user.password
    ) {
      alert('Login Successful');

      this.router.navigate(['/profile']);
    }
    else {
      alert('Invalid Email or Password');
    }
  }
}
```

**2. Open `src/app/login/login.html`** and replace the content with:
```html
<h2>Login User</h2>

Email:
<input type="email" [(ngModel)]="email">
<br><br>

Password:
<input type="password" [(ngModel)]="password">
<br><br>

<button (click)="loginUser()">
  Login
</button>
```

---

## Step 6: Profile Component
**1. Open `src/app/profile/profile.ts`** and replace the content with:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-profile',
  standalone: true,
  templateUrl: './profile.html',
  styleUrl: './profile.css'
})
export class ProfileComponent {

  user: any = {};

  ngOnInit() {

    let data =
      localStorage.getItem('user');

    this.user = JSON.parse(data!);
  }
}
```

**2. Open `src/app/profile/profile.html`** and replace the content with:
```html
<h2>User Profile</h2>

<p>
  <b>Name:</b> {{user.name}}
</p>

<p>
  <b>Email:</b> {{user.email}}
</p>
```

---

## Step 7: Run Application
Open your terminal inside the `ass3` project folder and run:

```bash
ng serve
```

Open your browser and naturally navigate to [http://localhost:4200](http://localhost:4200).

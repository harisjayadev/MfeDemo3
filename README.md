# Microfrontends Angular 

This project shows an example of using Webpack 5 Module Federation with Angular v11-next.5, note the use of **yarn**, this is required to override the webpack version for the angular cli

## Running the demo

- Install packages: `npm install`
- Start the mdmf-shell: `ng serve mdmf-shell`
- Start the Microfrontend: `ng serve mdmf-profile`
- Open the shell http://localhost:4200
- Click the profile navigation link to load the remote Microfrontend

## Project Structure

### Shell

The shell project located in: `projects/mdmf-shell` folder, its contains the shell application which is used to load remote Microfrontends using dynamic routing constructed from the Microfrontend array. The list of Microfrontends can be loaded from a config if required, but for the example it is just an hardcoded array.

### Profile Microfrontend

The profile project located in: `projects/mdmf-profile` contains a profile module with some child routes configured. The profile module is exposed as a remote module within the Module Federation config:

```js
plugins: [
  new ModuleFederationPlugin({
    name: 'profile',
    library: { type: 'var', name: 'profile' },
    filename: 'remoteEntry.js',
    exposes: {
      ProfileModule: './projects/mdmf-profile/src/app/profile/profile.module.ts',
    },
    shared: ['@angular/core', '@angular/common', '@angular/router'],
  }),
];
```

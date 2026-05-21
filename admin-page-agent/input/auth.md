# Auth

authType: bearer-token
tokenStorage: memory
permissionType:

routes:
  signIn: /sign-in
  signUp: /sign-up
  afterSignIn: /
  afterSignOut: /sign-in

mock:
  signUpEnabled: false
  seedUsers: []

actions: []

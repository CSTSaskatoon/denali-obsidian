## login form
```dart
Widget _buildLoginForm() {  
    final _formKey = GlobalKey<FormState>();  
    final Map<String, String> _formData = {};  
  
    return Form(  
        key: _formKey,  
        child: Flex(direction: Axis.horizontal, children: [  
          Column(  
            mainAxisSize: MainAxisSize.min,  
            children: [  
              TextFormField(  
                controller: _emailController,  
                decoration: const InputDecoration(  
                  labelText: 'Email',  
                  border: OutlineInputBorder(),  
                  errorStyle: TextStyle(color: Colors.red, fontSize: 12.0),  
                ),  
                keyboardType: TextInputType.emailAddress,  
                validator: (value) {  
                  if (value == null || value.isEmpty) {  
                    return 'Email is required';  
                  } else if (!isValidEmail(value)) {  
                    return 'Please enter a valid email';  
                  }  
                  return null;  
                },  
                onSaved: (value) => _formData['email'] = value?.trim() ?? '',  
              ),  
              const SizedBox(height: 10),  
              TextFormField(  
                controller: _passwordController,  
                decoration: InputDecoration(  
                  labelText: 'Password',  
                  border: const OutlineInputBorder(),  
                  suffixIcon: IconButton(  
                    icon: Icon(  
                      _passwordVisible  
                          ? Icons.visibility  
                          : Icons.visibility_off,  
                      semanticLabel:  
                          _passwordVisible ? 'Hide password' : 'Show password',  
                    ),  
                    onPressed: () {  
                      setState(() {  
                        _passwordVisible = !_passwordVisible;  
                      });  
                    },  
                  ),  
                ),  
                obscureText: !_passwordVisible,  
                validator: (value) {  
                  if (value == null || value.isEmpty) {  
                    return 'Password is required';  
                  }  
                  return null;  
                },  
                onSaved: (value) => _formData['password'] = value ?? '',  
              ),  
              // Reset Password Link (commented out because it's not working  
              // at the moment.)              // Align(              //   alignment: Alignment.centerRight,              //   child: TextButton(              //     onPressed: () {              //       // Navigate to PasswordResetPage              //       Navigator.push(              //         context,              //         MaterialPageRoute(builder: (context) => PasswordResetPage()),              //       );              //     },              //     child: const Text(              //       'Forgot Password?',              //       style: TextStyle(color: Colors.blue),              //     ),              //   ),              // ),              const SizedBox(height: 20),  
              if (_isLoading)  
                const Center(child: CircularProgressIndicator())  
              else  
                ElevatedButton(  
                  key: const ValueKey('loginButton'),  
                  onPressed: _isLoading  
                      // Disable button when loading  
                      ? null  
                      : () async {  
                          if (_formKey.currentState!.validate()) {  
                            _formKey.currentState!.save();  
                            // Start loading  
                            setState(() {  
                              _isLoading = true;  
                            });  
                            final authController = Provider.of<AuthController>(  
                                context,  
                                listen: false);  
                            final result = await authController.login(  
                                _formData['email']!,  
                                _formData['password']!,  
                                Role.THERAPIST);  
  
                            setState(() {  
                              _isLoading = false;  
                            });  
  
                            if (result != null &&  
                                result.containsKey('token') &&  
                                result.containsKey('therapistId')) {  
                              await authController.setToken(result['token']);  
                              await authController  
                                  .setTherapistId(result['therapistId']);  
                              Navigator.pushNamed(context, '/profile');  
                            } else {  
                              ScaffoldMessenger.of(context).showSnackBar(  
                                SnackBar(  
                                    content: Text(  
                                        result?['message'] ?? 'Login failed.')),  
                              );  
                            }  
                          }  
                        },  
                  child: const Text('Login'),  
                ),  
            ],  
          ),  
          Column(mainAxisSize: MainAxisSize.min, children: [  
            
          ])  
        ]));  
  }  
```
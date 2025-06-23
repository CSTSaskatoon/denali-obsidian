**Scrapped test for because it depends on therapist auth**
```flutter
testWidgets(  
    'Therapist can not restore patients not under them in the recycle bin',  
    (tester) async {  
  var patientId =  
      'patient-who-should-not-be-deleted-test- 3002f8ee-59f5-4bad-8e57-bdee75e67079';  
  
  await login(tester, therapistEmail2, therapistPassword);  
  await navigateToPatientList(tester);  
  
  var response = await http.post(  
      Uri.parse('$address:$port/$patientsRoute/recycle/$patientId'),  
      headers: {  
        "Content-Type": "application/json",  
        // TODO I think I need to pass this the bearer token or something  
      });  
  // 401 - Unauthorized  
  expect(401, response.statusCode);  
});
```

**May need test for if a patient is restored while the therapist is deleted**

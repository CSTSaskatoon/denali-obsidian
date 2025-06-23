### `RegisterOwner()`
```cs
[HttpPost("owner/register")]  
public async Task<IActionResult> RegisterOwner([FromBody] OwnerRegistrationRequest req)  
{  
    try  
    {  
        if (!ModelState.IsValid)  
        {  
            Console.WriteLine("ModelState is invalid.");  
            foreach (var error in ModelState.Values.SelectMany(v => v.Errors))  
            {  
                Console.WriteLine($"Validation Error: {error.ErrorMessage}");  
            }  
  
            return BadRequest(ModelState);  
        }  
  
        // Use the Firebase Authentication Emulator to create the user  
        var firebaseAuthUrl = "http://localhost:9099/identitytoolkit.googleapis.com/v1/accounts:signUp?key=fake-key";  
  
        var payload = new  
        {  
            email = req.Email,  
            password = req.Password,  
            returnSecureToken = true  
        };  
  
        using var client = new HttpClient();  
        var response = await client.PostAsync(  
            firebaseAuthUrl,  
            new StringContent(JsonConvert.SerializeObject(payload), Encoding.UTF8, "application/json")  
        );  
  
        var responseContent = await response.Content.ReadAsStringAsync();  
          
        // Check if the registration request to the emulator was successful  
        if (!response.IsSuccessStatusCode)  
        {  
            var errorResponse = JObject.Parse(responseContent);  
            var errorMessageCode = errorResponse["error"]?["message"]?.ToString();  
  
            if (errorMessageCode == "EMAIL_EXISTS")  
            {  
                Console.WriteLine("Registration failed: Email is already registered.");  
                return BadRequest(new { Message = "Email is already registered." });  
            }  
  
            Console.WriteLine("Registration failed: Unable to create user in Firebase Auth Emulator.");  
            return BadRequest(new { Message = "Failed to register user. Please try again later." });  
        }  
  
          
          
        var authResponse = JObject.Parse(responseContent);  
        // Console.WriteLine($"Full Auth Response: {authResponse}");  
        // Get the UID of the newly created user        var uid = authResponse["localId"]?.ToString();  
        Console.WriteLine($"UID from registration: {uid}");  
  
        // Check if the user exists in Firebase  
        try  
        {  
            var userRecord = await FirebaseAuth.DefaultInstance.GetUserAsync(uid);  
            if (userRecord == null)  
            {  
                Console.WriteLine($"User with UID {uid} does not exist in Firebase.");  
            }  
            else  
            {            }        }  
        catch (FirebaseAuthException ex)  
        {  
            Console.WriteLine($"Firebase Auth Exception: {ex.Message}");  
        }  
        
        var owner = new Owner  
        {  
            OwnerId = uid,  
            FName = req.FName,  
            LName = req.LName,  
            Email = req.Email,
        };  
  
        var docRef = _firestore.Collection(OwnerController.COLLECTION_NAME).Document(uid);  
        await docRef.SetAsync(owner);  
  
        Console.WriteLine("Owner data saved in Firestore.");  
  
        // Success response  
        return Ok(new { Message = "Owner registered successfully!", UID = uid });  
    }  
    catch (Exception ex)  
    {  
        Console.WriteLine($"Error: {ex.Message}");  
        return BadRequest(new { Message = "An unexpected error occurred during registration. Please try again later." });  
    }  
  
}
```

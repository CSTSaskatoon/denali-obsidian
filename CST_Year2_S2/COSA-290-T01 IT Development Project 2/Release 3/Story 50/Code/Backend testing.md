## Owner therapist seed data
```cs
public static async Task SeedOwnerInfoLoginAndTherapistListPage(FirestoreDb firestoreDb)  
{  
    _firestoreDb = firestoreDb;  
    _ownerController = new OwnerController(_firestoreDb);  
    _therapistController = new TherapistController(_firestoreDb);  
  
    var owner1Email = "johndoe1@test.com";  
    var owner2Email = "johndoe2@test.com";  
      
    var firebaseAuthUrl =  
        "http://localhost:9099/identitytoolkit.googleapis.com/v1/accounts:signUp?key=fake-key";  
  
    var owner1Payload = new  
    {  
        email = owner1Email,  
        password = "Password1!",  
        returnSecureToken = true  
    };  
  
    using var client = new HttpClient();  
    await client.PostAsync(  
        firebaseAuthUrl,  
        new StringContent(JsonConvert.SerializeObject(owner1Payload), Encoding.UTF8, "application/json")  
    );  
      
    var owner2Payload = new  
    {  
        email = owner2Email,  
        password = "Password1!",  
        returnSecureToken = true  
    };  
  
    await client.PostAsync(  
        firebaseAuthUrl,  
        new StringContent(JsonConvert.SerializeObject(owner2Payload), Encoding.UTF8, "application/json")  
    );  
  
    // Add the owners  
    var ownerCollection = _firestoreDb.Collection(OwnerController.COLLECTION_NAME);  
  
    var owner1 = new Owner()  
    {  
        OwnerId = owner1Id,  
        Email = owner1Email,  
        FName = "John",  
        LName = "Doe"  
    };  
  
    var owner2 = new Owner()  
    {  
        OwnerId = owner2Id,  
        Email = owner2Email,  
        FName = "John",  
        LName = "Doe"  
    };  
  
    await ownerCollection.Document(owner1Id).SetAsync(owner1);  
    await ownerCollection.Document(owner2Id).SetAsync(owner2);  
  
    // Add the therapists under the owners (therapists Collection nested in owners Collection)  
    var owner1TherapistCollection =  
        ownerCollection.Document(owner2Id).Collection(TherapistController.COLLECTION_NAME);  
    var owner2TherapistCollection =  
        ownerCollection.Document(owner2.OwnerId).Collection(TherapistController.COLLECTION_NAME);  
  
    var owner1Therapist1 = new Therapist()  
    {  
        TherapistID = "testOwner1therapist1",  
        Email = "johnsmith1@test.com",  
        FName = "John 1",  
        LName = "Smith 1"  
    };  
  
    var owner1Therapist2 = new Therapist()  
    {  
        TherapistID = "testOwner1therapist2",  
        Email = "johnsmith2@test.com",  
        FName = "John 1",  
        LName = "Smith 2"  
    };  
  
    var owner2Therapist1 = new Therapist()  
    {  
        TherapistID = "testOwner2therapist1",  
        Email = "janesmith1@test.com",  
        FName = "Jane 2",  
        LName = "Smith 1"  
    };  
  
    var owner2Therapist2 = new Therapist() // Has no patients under them  
    {  
        TherapistID = "testOwner2therapist2",  
        Email = "janesmith2@test.com",  
        FName = "Jane 2",  
        LName = "Smith 2"  
    };  
  
    await owner1TherapistCollection.AddAsync(owner1Therapist1);  
    await owner1TherapistCollection.AddAsync(owner1Therapist2);  
    await owner2TherapistCollection.AddAsync(owner2Therapist1);  
    await owner2TherapistCollection.AddAsync(owner2Therapist2);  
      
    // Register the owner accounts to firebase auth  
      
    Therapist[] therapists =  
    {  
        owner1Therapist1, owner2Therapist1, owner1Therapist2  
    };  
    await SeedPatientInfoForTherapistListPage(therapists);  
}  
  
public static async Task SeedPatientInfoForTherapistListPage(Therapist[] therapists)  
{  
    for (int i = 0; i < therapists.Length; i++)  
    {  
        var patientCollection = _firestoreDb.Collection(TherapistController.COLLECTION_NAME)  
            .Document(therapists[i].TherapistID).Collection(PatientController.COLLECTION_NAME);  
  
        var patienta = new PatientPrivate()  
        {  
            Id = $"patient{i}a",  
            TherapistID = therapists[i].TherapistID,  
            Condition = "Autism",  
            FName = $"Joe {i}",  
            LName = "Schmoe a",  
            Phone = "123-456-7890",  
            Age = 15,  
            Weight = 60,  
            Height = 150,  
            Email = $"joeshchmoe{i}a@test.com",  
            DoctorPhoneNumber = "123-456-7890",  
            GuardianPhoneNumber = "123-456-7890"  
        };  
          
        var patientb = new PatientPrivate()  
        {  
            Id = $"patient{i}b",  
            TherapistID = therapists[i].TherapistID,  
            Condition = "Autism",  
            FName = $"Joe {i}",  
            LName = "Schmoe b",  
            Phone = "123-456-7890",  
            Age = 15,  
            Weight = 60,  
            Height = 150,  
            Email = $"joeshchmoe{i}b@test.com",  
            DoctorPhoneNumber = "123-456-7890",  
            GuardianPhoneNumber = "123-456-7890"  
        };  
          
        patientCollection.AddAsync(patienta).Wait();  
        patientCollection.AddAsync(patientb).Wait();  
    }  
}
```
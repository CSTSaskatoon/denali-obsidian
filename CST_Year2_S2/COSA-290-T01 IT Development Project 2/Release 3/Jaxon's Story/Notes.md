# Notes
### ATP
Might want to move the "Valid therapist registration data" to the top

### Class Diagrams
#### Backend
`authcontroller.cs` should have the following added (mermaid syntax)
- `+GetUserByEmail(string email) Task<IActionResult>` - also in this method you should have `[FromRoute] string email` in the method header, and for the route do `[HttpGet("users/{email}")]` instead of `[HttpGet("users/{uid}"]`

#### Frontend
- No changes

### Sequence
```mermaid
sequenceDiagram
	actor t as Therapist
	participant regpage as registration_page
	participant authcon as auth_controller
	participant AuthConBE as AuthController
	participant FBA as FirebaseAuth
	participant SMTP as SmtpClient

	t ->>+ regpage: Clicks 'register' button
	regpage -) authcon: RegisterTherapist(therapist, password)
	authcon -) AuthConBE: RegisterTherapist(therapistRegistrationReq)
	AuthConBE -) AuthConBE: SendVerfEmail(req.Email)
	AuthConBE -) FBA: GenerateEmailVerificationLinkAsync(email)
	FBA --) AuthConBE: Task<string>
	AuthConBE --) AuthConBE: Task<string>
	AuthConBE ->>+ SMTP: Send(from, to, subject, body)
	SMTP -->> t: Sends verification link via email
	AuthConBE --) AuthConBE: Task<IActionResult>
	AuthConBE --) authcon: Task<IActionResult>
	authcon --) regpage: Future<String?>
	t ->>+ t: clicks link in email
```

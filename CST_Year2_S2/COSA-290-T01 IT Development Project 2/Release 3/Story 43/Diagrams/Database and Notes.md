### Story Notes
- Need to keep the recycled patient's ID and info until the recycle bin expires (probably 90 days)
- Patient info not in `PatientPrivate` needs to be saved
- Need to keep the patient's ID in session/evaluation objects so they can be properly restored, and even after the 90 days it should stay as the data is generic
- Would be good to make a `Recycleable` interface so that it is easier to add functionality for restoring therapists and other things in the future
- Want a generic `recycleItem` widget on the frontend that has a restore and delete button
- **What if a patient gets deleted, therapist is deleted, and patient is restored**
	- Delete the therapist anyways, when you go to restore the patient, check if the therapist exists
	- If the therapist doesn't exist, add them to the `pruned-patients` collection at root

Basically I think I need to make a `deleted-patients` collection with an object that inherits from `PatientPrivate` and also maybe an interface `Recycleable`?

### Pre-code Notes
**People are working on**
- Me - patients in the recycle bin
- Seth - Just finished his graph story, therapist authorization story that was not completed last week by Shane
- Shane - Therapist saves data locally until network is restored
- Jaxon - Email verification
- Gia - edit and delete therapists under them
- Aron - Owner transfers patients from one therapist to another

**Things that need fixing**
- Need tests for evals and sessions of patient remaining even after permanently deleting the patient from recycle bin

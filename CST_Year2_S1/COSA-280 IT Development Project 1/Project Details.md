>Date: 2024 09 03
>Author: Denali Therrien
>Teachers: Wade Lahoda, Ernesto Basalto

### Hippotherapy session tracker
Details found [here](https://online.saskpolytech.ca/d2l/le/content/353894/viewContent/14387475/View)
Hippotherapy is a physical, occupational, and speech therapy that utilizes the natural gait and movement of a horse to provide motor and sensory input. It is based on improvement of neurologic functions, and sensory processes, and used for patients with physical and mental disorders. ([What is hippotherapy? The indications and effectiveness of hippotherapy - PMC (nih.gov)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5175116/#:~:text=Hippotherapy%20is%20a%20physical%2C%20occupational,with%20physical%2C%20and%20mental%20disorders.))

We have partnered with several therapists around the world to standardize the assessment and track patients’ progress as they undergo hippotherapy. For that reason, we have commissioned a survey like application to assess patients before and after each therapy session.

This is a continuation of a project from the Software Developer Certificate program. Most of the therapist assessment user interface is complete and some aspects like authentication and offline data storage and synchronization are still required

*Goals*
- Download/Export data from the central database for further analysis using common statistics software 
- Internationalize the text for multiple languages
- Ability to store assessment data offline until the device has internet connectivity and can synchronize with an online central database.

#### Technologies
- Frontend will probably be react
- Back-end probably C# or Java and Postgres or MongoDB (MongoDB is noSQL so it would be much different to work with and would take some getting used to)
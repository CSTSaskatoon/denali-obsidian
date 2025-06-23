# Scenarios
## Scenario 1
- Saskpolytech
- 6 Locations

### Start with One domain
- `saskpolytech.ca`
- `Admin`
- `DICE`
- `Campus_SN`
- `CST`
- Add a second DC to the domain for redundancy

## Scenario 2
- saskpolytech
- 6 locations
- CST and CAD require separate admins but common namespace

### Start with one domain
- `saskpolytech.ca`
- `ADMIN`
- `DICE`
- `CAMPUS_SN`
- Create a subdomain - `cst.saskpolytech.ca`
- Create another subdomain - `cad.saskpolytech.ca`

## Scenario 2
- saskpolytech
- 6 locations
- CST and CAD require separate admins but common namespace
- DICE requires separate admins and namespace

### Start with One domain
- Add cst and cad subdomains
- Create a new tree in the forest
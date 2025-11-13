# Comprehensive Founding Members Search - Claude Desktop/Claude.ai

**Use Claude Desktop or Claude.ai with browser access for this task**

---

## MISSION

Conduct a comprehensive search of UK registries AND open web sources to find ALL organizational affiliations for 9 founding members of BLKOUT Community Benefit Society.

**Goal**: Complete disclosure for FCA registration within 7 days.

**Why this matters**: Our manual search found 6 Companies House appointments but MISSED at least one known CIC directorship. We need YOU to find everything we missed using browser access.

---

## SEARCH ALL 9 MEMBERS ACROSS ALL REGISTRIES

For EACH person below, search:

1. **Companies House** (https://find-and-update.company-information.service.gov.uk/search/officers)
   - Current AND resigned directorships
   - All company types: Ltd, PLC, CIC, LLP
   - Check variant names (with/without middle names, hyphenated surnames)

2. **Charity Commission** (https://register-of-charities.charitycommission.gov.uk/)
   - Trustee positions (current and recent)
   - Search charity names if person mentions any
   - Download recent charity accounts to check trustee lists

3. **FCA Mutuals Register** (https://mutuals.fca.org.uk/)
   - Cooperative and Community Benefit Society officer positions
   - Search both by person name and organization name

4. **LinkedIn** (if accessible)
   - Current positions listed
   - Board memberships
   - Company affiliations
   - Verify against registry findings

5. **General Web Search**
   - "[Full Name]" + "director" + "UK"
   - "[Full Name]" + "trustee" + "charity"
   - "[Full Name]" + "cooperative" OR "co-op"
   - Company director check sites (checkcompany.co.uk, companydirectorcheck.com, etc.)

---

## THE 9 FOUNDING MEMBERS

### 1. Robert Berkeley
- **Birth**: March 1974
- **Address**: [Not provided - search all UK]
- **Known affiliation**: CIC directorship (name unknown - FIND IT!)
- **Our search found**: Nothing (but we know there's at least 1 CIC)

**Your mission**: Find the CIC we missed + any other affiliations

---

### 2. Jean-Eric Nkurikiye
- **Birth**: December 1976
- **Address**: Hackney, London
- **Our search found**: 1 Companies House appointment (company name unknown)

**Your mission**:
- Find the 1 company name/details
- Check for charities, co-ops, other companies

---

### 3. Lloyd Young
- **Birth**: February 1965
- **Address**: [Not provided - search all UK]
- **Our search found**: Nothing (closest: Lloyd Young born October 1965)

**Your mission**:
- Verify truly no directorships OR find under different birth month
- Check charities, co-ops

---

### 4. Nathan Lewis
- **Birth**: September 1985
- **Address**: [Not provided - search all UK]
- **Our search found**: Nothing

**Your mission**:
- Very common name - use birth date to filter
- Check all registries

---

### 5. Olamide Adesanya
- **Birth**: August 1990
- **Address**: Flat 3 Whitmore House, East Crescent, London, England, N11 3AU
- **Our search found**: 3 Companies House appointments
  - THE REEL HAPPY HOUR PODCAST SHOW LTD (14499903) - Active
  - VARSITY REIGN CLOTHING LTD (13081070) - Dissolved
  - 3rd appointment unknown

**Variant name to check**: Olamide Abdul-Afeez ADESANYA

**Your mission**:
- Find the 3rd company name/details
- Verify the 2 we found are correct
- Check for charities, co-ops

---

### 6. Peter Fleming
- **Birth**: December 1967
- **Address**: [Not provided - search all UK]
- **Our search found**: Nothing (extremely common name - 208,390 results)

**Your mission**:
- Very common name - birth date critical for filtering
- Check all registries

---

### 7. Reuben Silungwe
- **Birth**: August 1980
- **Address**: [Not provided - search all UK]
- **Our search found**: Nothing (distinctive name but no matches)

**Your mission**:
- Unusual name - if nothing in registries, likely truly nothing
- But check charities and co-ops (not just Companies House)

---

### 8. Cardew Olanrewaju Jackson-Cole
- **Birth**: July 1982
- **Address**: 86 The Avenue, Corby, England, NN17 5EE
- **Our search found**: 1 Companies House appointment (company name unknown)

**Name variants to check**:
- Cardew Jackson-Cole
- Cardew Olanrewaju Jackson-Cole
- Cardew Jackson Cole (no hyphen)

**Your mission**:
- Find the 1 company name/details
- Check for charities, co-ops

---

### 9. Gerrard Martin
- **Birth**: June 1975
- **Address**: 19 Claremont Street, Greenwich, London, United Kingdom, SE10 9LH
- **Our search found**: 1 Companies House appointment (company name unknown)

**Name variants to check**:
- Gerrard Martin
- Gerard Martin
- Gerald Martin

**Your mission**:
- Find the 1 company name/details
- Check for charities, co-ops

---

## OUTPUT FORMAT

For EACH person, provide:

```markdown
## [MEMBER NAME]

### Companies House
[If found]
1. Company Name: [NAME]
   Registration Number: [NUMBER]
   Role: [Director/Secretary/etc.]
   Appointed: [DD/MM/YYYY]
   Resigned: [DD/MM/YYYY or "Current"]
   Company Status: [Active/Dissolved/Liquidation/etc.]

[If NOT found]
❌ No Companies House appointments found
   Search attempted: [Describe what you searched - name variants, filters used]

### Charity Commission
[If found]
1. Charity Name: [NAME]
   Registration Number: [NUMBER]
   Role: [Trustee/Secretary/etc.]
   Appointed: [Year or "Unknown"]
   Status: [Active/Removed]

[If NOT found]
❌ No Charity Commission trusteeships found
   Search attempted: [Describe search]

### FCA Mutuals Register
[If found]
1. Society Name: [NAME]
   Registration Number: [NUMBER]
   Role: [Committee member/Secretary/etc.]
   Appointed: [Year]

[If NOT found]
❌ No FCA Mutuals appointments found
   Search attempted: [Describe search]

### Other Findings (LinkedIn, Web Search, etc.)
[Any additional information found]

### SUMMARY FOR THIS MEMBER
Total affiliations found: [NUMBER]
Confidence level: [High/Medium/Low - based on search thoroughness]
Recommended action: [e.g., "Confirm with member", "Likely complete", "Needs member input"]
```

---

## SPECIAL INSTRUCTIONS

### For Robert Berkeley
**CRITICAL**: We KNOW he has a CIC directorship that our search missed. Your primary goal is to FIND IT.

Try:
- All name variants (Robert Berkeley, R Berkeley, Rob Berkeley, etc.)
- Different birth date filters (maybe recorded wrong)
- Check CIC-specific searches
- LinkedIn for current board positions
- Web search for "Robert Berkeley" + "CIC" + "director"

### For members with "1 appointment found" but unknown company
**Jean-Eric, Cardew, Gerrard** - When you find their officer page on Companies House:
- Click through to their full appointment history
- Note ALL appointments (current AND resigned)
- We said "1" but there might be more - get complete list

### For Olamide's 3rd appointment
Check under both:
- Olamide ADESANYA
- Olamide Abdul-Afeez ADESANYA

Same address (N11 3AU) - might be listed differently

### Search Efficiency Tips
1. **Start with Companies House** - most comprehensive, easiest to search
2. **Charity Commission is harder** - no direct trustee search, may need to search individual charities
3. **FCA Mutuals** - limited public searchability, focus on known society names
4. **Cross-reference** - If you find someone is a director of "XYZ Community CIC", search that CIC in Charity Commission in case it's dual-registered
5. **Use birth dates** - Critical for filtering common names (Lloyd Young, Nathan Lewis, Peter Fleming)

---

## WHAT WE NEED MOST

**Priority 1** (CRITICAL):
1. Robert Berkeley's missing CIC
2. Company names for Jean-Eric, Cardew, Gerrard
3. Olamide's 3rd company

**Priority 2** (Important):
1. Charity trusteeships for ALL members (we haven't searched this yet)
2. FCA Mutuals/co-op positions for ALL members
3. Verification that the 5 members with "no appointments" truly have none

**Priority 3** (Nice to have):
1. Resigned/dissolved company directorships (last 3 years)
2. LinkedIn verification of current roles
3. Any sole trader or partnership information

---

## TIME ESTIMATE

- **Quick search** (Companies House only, 4 members with known appointments): 15-20 minutes
- **Thorough search** (All 9 members, Companies House + Charity + FCA + web): 60-90 minutes
- **Comprehensive search** (Everything + LinkedIn + deep web search): 2-3 hours

**Recommended**: Start with Priority 1 (30-45 min), then Priority 2 if time permits.

---

## FINAL CHECKLIST

Before you finish, verify:

- [ ] Searched all 9 members in Companies House
- [ ] Searched all 9 members in Charity Commission
- [ ] Searched all 9 members in FCA Mutuals
- [ ] Found Robert Berkeley's missing CIC
- [ ] Found company names for Jean-Eric, Cardew, Gerrard
- [ ] Found Olamide's 3rd company
- [ ] Cross-referenced findings with LinkedIn where possible
- [ ] Provided complete details (not just "1 appointment" but actual company names/dates)
- [ ] Noted confidence level for each member
- [ ] Flagged any that need member follow-up

---

## RETURN YOUR FINDINGS

Paste the full results using the format above for all 9 members.

**Include**:
- What you found (with complete details)
- What you searched (so we know you tried)
- What's missing (so we know what to ask members)
- Recommended next steps

**CRITICAL**: We have 7 days to submit to FCA. Your search results will be combined with direct member outreach to create complete disclosure.

---

**Good luck! You're helping BLKOUT get its legal foundation in place.** 🚀

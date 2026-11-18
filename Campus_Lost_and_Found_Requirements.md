# Campus Lost & Found

## Project Requirements Specification

**Project type:** Beginner-friendly Python team project\
**Workshop duration:** 90 minutes\
**Audience:** Students with mixed levels of Python experience\
**Application type:** Command-line application (CLI)\
**Storage:** Local JSON file\
**External dependencies:** None required

------------------------------------------------------------------------

## 1. Project Overview

Campus Lost & Found is a small Python application that helps students
report belongings they have lost or found on campus. Users can register
lost or found items, search existing reports, view all reports, and mark
an item as recovered.

The project demonstrates how Python fundamentals can be combined to
build a practical software application. It is intended as a learning
prototype, not a production-ready campus service.

## 2. Problem Statement

Students may lose items such as identity cards, wallets, keys, water
bottles, notebooks, chargers, and other personal belongings around
campus. Information about lost and found items is often shared
informally through messages, notice boards, or word of mouth.

The application provides one simple place to record and search these
reports.

## 3. Project Objectives

-   Apply Python concepts to a relatable real-world problem.
-   Practise functions, loops, conditionals, lists, dictionaries, and
    modules.
-   Read and write structured data using JSON.
-   Introduce input validation and exception handling.
-   Introduce basic software design, testing, debugging, and Git
    collaboration.
-   Deliver a working command-line prototype within a 90-minute team
    workshop.

## 4. Scope

### In scope

-   Register a lost item.
-   Register a found item.
-   Search reports by keyword.
-   View all reports.
-   Mark a report as recovered.
-   Save records locally in a JSON file.
-   Load saved records when the application starts.
-   Validate basic user input and handle common errors.

### Out of scope for the first version

-   User accounts, login, or authentication.
-   Online or cloud database.
-   Multiple users accessing a shared live database.
-   Image uploads.
-   Email, SMS, or push notifications.
-   Automatic matching or AI recommendations.
-   Maps or GPS tracking.
-   Web or mobile interface.
-   Production-grade security, privacy controls, or deployment.

These can be considered as future extensions.

## 5. Users and Usage

The first version is a local CLI prototype operated by a student through
a terminal. It does not distinguish between individual users or
authenticate who submits a report.

Typical use cases:

1.  A student loses a wallet and submits a lost-item report.
2.  A student finds a phone and submits a found-item report.
3.  A student searches for an item by its name, category, or location.
4.  A student views all reports to check whether an item has been
    reported.
5.  A student marks a report as recovered after the item is returned.

## 6. Functional Requirements

### FR-01: Main menu

The application shall display a menu with these options:

1.  Report Lost Item
2.  Report Found Item
3.  Search Items
4.  View All Items
5.  Mark Item as Recovered
6.  Exit

The application shall ask the user to select an option. An invalid
option shall display an error message and return to the menu without
crashing.

### FR-02: Report a lost item

The application shall allow a user to create a report with the status
`lost`.

The application shall collect:

-   Item name (required)
-   Category (required)
-   Location where the item was last seen (required)
-   Description (optional)

The application shall generate a unique numeric ID and record the date
and time of submission.

After successful submission, the application shall save the report and
display a confirmation message and the report ID.

### FR-03: Report a found item

The application shall allow a user to create a report with the status
`found`.

The application shall collect:

-   Item name (required)
-   Category (required)
-   Location where the item was found (required)
-   Description (optional)

The application shall generate a unique numeric ID and record the date
and time of submission.

After successful submission, the application shall save the report and
display a confirmation message and the report ID.

### FR-04: Search reports

The application shall allow a user to search reports using a text
keyword.

The keyword shall be matched case-insensitively against:

-   Item name
-   Category
-   Location
-   Description

The application shall display all matching records. If no record
matches, it shall display a clear "No matching items found" message.

An empty search keyword shall be rejected with a helpful message.

### FR-05: View all reports

The application shall display all stored reports, including:

-   ID
-   Name
-   Category
-   Location
-   Description
-   Status
-   Date and time

If there are no reports, the application shall display a message
indicating that no records are available.

### FR-06: Mark an item as recovered

The application shall allow a user to enter a report ID and mark the
corresponding report as `recovered`.

The application shall:

-   Reject non-numeric IDs.
-   Display an error if the ID does not exist.
-   Inform the user if the item is already recovered.
-   Save the updated status to the JSON file.
-   Confirm when the update succeeds.

### FR-07: Persistent storage

The application shall store records in a local file named `items.json`.

The application shall load records from the file at startup.

Changes shall be saved after a report is created or a report status is
updated. Data shall remain available after the application is closed and
restarted.

If the data file does not exist on first launch, the application shall
start with an empty list of records.

If the JSON file is malformed or cannot be read, the application shall
show a clear error rather than silently overwriting the existing data.

## 7. Data Requirements

Each item shall be represented as a Python dictionary and stored as a
JSON object.

### Required record structure

``` json
{
  "id": 1,
  "name": "Black Wallet",
  "category": "Accessories",
  "location": "Library",
  "description": "Contains college ID",
  "status": "lost",
  "date": "2026-11-18 10:30:00"
}
```

### Field definitions

  Field           Type        Required Description
  --------------- --------- ---------- --------------------------------------
  `id`            Integer          Yes Unique report identifier
  `name`          String           Yes Name of the item
  `category`      String           Yes Item category
  `location`      String           Yes Relevant campus location
  `description`   String            No Additional identifying details
  `status`        String           Yes `lost`, `found`, or `recovered`
  `date`          String           Yes Date and time the report was created

### Data rules

-   IDs must be unique within the stored dataset.
-   New IDs should be generated from the highest existing ID plus one.
-   Status must be one of `lost`, `found`, or `recovered`.
-   Required text fields must not be empty or consist only of spaces.
-   Search should ignore letter case.
-   The JSON file should contain a top-level array of records.

## 8. Non-Functional Requirements

### NFR-01: Usability

-   The menu and prompts shall use clear, beginner-friendly language.
-   Errors shall explain what went wrong and, where possible, how to
    correct it.
-   The application shall return to the main menu after an operation.

### NFR-02: Reliability

-   Invalid menu choices and invalid IDs shall not crash the
    application.
-   Missing data files shall be handled.
-   Malformed JSON shall be reported clearly.
-   Data shall be saved after successful changes.

### NFR-03: Maintainability

-   Code shall be separated into modules by responsibility.
-   Functions shall have clear names and focused responsibilities.
-   The project shall use consistent naming and readable formatting.

### NFR-04: Portability

-   The application should run on Windows, macOS, and Linux with Python
    3.
-   The application should use Python's standard library only.
-   File paths should work across supported operating systems.

### NFR-05: Performance

-   The application is designed for a small workshop-scale dataset.
-   Searching may use a simple linear scan through the records.
-   No database server or network connection is required.

## 9. Technology Requirements

  Component                  Technology
  -------------------------- --------------------------------------------
  Programming language       Python 3
  User interface             Command-line interface
  Data format                JSON
  Storage                    Local file (`items.json`)
  Standard library modules   `json`, `os`, `datetime`
  Code editor                VS Code, PyCharm, or another Python editor
  Version control            Git
  Collaboration platform     GitHub

No `pip install` step is required for the basic application.

## 10. Proposed Project Structure

``` text
campus-lost-found/
├── main.py
├── item_manager.py
├── search.py
├── storage.py
├── items.json
├── README.md
└── .gitignore
```

### Module responsibilities

  -----------------------------------------------------------------------
  File                                Responsibility
  ----------------------------------- -----------------------------------
  `main.py`                           Displays the menu, handles choices,
                                      and connects modules

  `item_manager.py`                   Creates lost/found reports and
                                      marks reports recovered

  `search.py`                         Searches records and displays item
                                      details

  `storage.py`                        Loads and saves JSON data

  `items.json`                        Stores application records

  `README.md`                         Explains the project and how to run
                                      it

  `.gitignore`                        Excludes generated and local-only
                                      files from Git
  -----------------------------------------------------------------------

## 11. Application Architecture

The application follows a simple modular architecture:

``` text
                  USER
                    |
                    v
           COMMAND-LINE MENU
                main.py
                    |
          +---------+----------+
          |         |          |
          v         v          v
      ITEM       SEARCH     DATA STORAGE
    MANAGEMENT   & DISPLAY    storage.py
 item_manager.py  search.py       |
          |         |             |
          +---------+-------------+
                    |
                    v
               items.json
           (persistent records)
```

### Data flow

1.  The user selects an action from the menu.
2.  `main.py` calls the appropriate module function.
3.  The function validates input and performs the requested operation.
4.  The storage module reads or writes `items.json` when needed.
5.  The application displays the result to the user.

## 12. Team Roles

Recommended team size: four students.

  -----------------------------------------------------------------------
  Team member             Responsibility          Deliverable
  ----------------------- ----------------------- -----------------------
  Member 1                Application flow        Main menu and user
                                                  interaction

  Member 2                Data management         Item record creation
                                                  and JSON storage

  Member 3                Search and validation   Search functionality
                                                  and input checks

  Member 4                Integration and testing Module integration,
                                                  test execution, and
                                                  README
  -----------------------------------------------------------------------

All members should understand the overall application and participate in
the final demonstration.

## 13. Workshop Schedule (90 Minutes)

  -----------------------------------------------------------------------
  Time                    Activity                Expected outcome
  ----------------------- ----------------------- -----------------------
  0--10 min               Introduce the problem   Students understand the
                          and demonstrate the     use case
                          target application      

  10--20 min              Review relevant Python  Students recall
                          concepts                required syntax

  20--30 min              Explain architecture,   Teams understand the
                          files, and team         design
                          responsibilities        

  30--60 min              Team development sprint Core features
                                                  implemented

  60--75 min              Testing and debugging   Main workflows verified

  75--90 min              Team demonstrations and Teams explain and
                          wrap-up                 demonstrate their work
  -----------------------------------------------------------------------

## 14. Acceptance Criteria

The project is considered complete for the workshop when:

-   [ ] The application starts using `python main.py` or
    `python3 main.py`.
-   [ ] The main menu displays all six options.
-   [ ] A lost-item report can be created.
-   [ ] A found-item report can be created.
-   [ ] Each new report receives a unique ID.
-   [ ] Reports include a date and time.
-   [ ] Reports are saved to `items.json`.
-   [ ] Existing reports load when the application restarts.
-   [ ] Search works by name, category, location, and description.
-   [ ] Search is case-insensitive.
-   [ ] A no-results message is displayed when appropriate.
-   [ ] All reports can be viewed.
-   [ ] A report can be marked as recovered using its ID.
-   [ ] Invalid menu choices and invalid IDs are handled.
-   [ ] Empty required fields are rejected.
-   [ ] The application does not silently replace corrupted JSON data.
-   [ ] The team can explain the purpose of each Python module.

## 15. Test Scenarios

  -----------------------------------------------------------------------
  Test ID                 Scenario                Expected result
  ----------------------- ----------------------- -----------------------
  T-01                    Start the application   Application starts with
                          with no `items.json`    an empty dataset
                          file                    

  T-02                    Submit a valid          Report is saved with
                          lost-item report        status `lost`

  T-03                    Submit a valid          Report is saved with
                          found-item report       status `found`

  T-04                    Leave the item name     Report is rejected
                          blank                   

  T-05                    Search for an existing  Matching record is
                          item name               displayed

  T-06                    Search using different  Matching record is
                          letter case             still found

  T-07                    Search for an unknown   No-results message is
                          item                    displayed

  T-08                    View reports when       All records are
                          records exist           displayed

  T-09                    Restart after saving a  Previously saved record
                          report                  is loaded

  T-10                    Enter a non-numeric     Helpful validation
                          recovery ID             message is displayed

  T-11                    Enter an unknown        Item-not-found message
                          recovery ID             is displayed

  T-12                    Recover an existing     Status changes to
                          report                  `recovered` and is
                                                  saved

  T-13                    Enter an invalid menu   Error is displayed and
                          choice                  menu continues

  T-14                    Start with malformed    Clear storage error is
                          JSON                    displayed; data is not
                                                  silently overwritten
  -----------------------------------------------------------------------

## 16. Git and GitHub Collaboration Requirements

Teams should use Git to track their work.

Suggested workflow:

1.  Create one GitHub repository for the team.
2.  Add team members as collaborators.
3.  Agree on file names and function interfaces before coding.
4.  Assign ownership of modules.
5.  Commit small, meaningful changes.
6.  Integrate modules and resolve any import or interface issues.
7.  Run the complete application before presenting.

Example commands:

``` bash
git init
git add .
git commit -m "Create project structure"
git branch
git remote add origin <repository-url>
git push -u origin main
```

For a 90-minute beginner workshop, keep collaboration simple. Branches
and pull requests can be demonstrated as an optional introduction if
time permits.

## 17. Optional Extension Challenges

These are not required for the first working version.

### Easy

-   Display counts of lost, found, and recovered reports.
-   Search by report ID.
-   Add a confirmation before marking a report recovered.
-   Sort reports by submission date.

### Medium

-   Filter reports by status.
-   Filter reports by date.
-   Add duplicate-report checks.
-   Allow users to edit a report.
-   Add a simple report summary.

### Advanced / Future Version

-   Build a web interface using Flask.
-   Build a REST API using FastAPI.
-   Replace JSON storage with SQLite.
-   Add student authentication.
-   Add image uploads.
-   Add notifications.
-   Add automated matching between lost and found reports.

## 18. Limitations and Responsible Use

-   This is a local learning prototype. Data is stored on the computer
    running the application.
-   It does not provide a shared campus-wide database.
-   Reports are not verified, and the application cannot prove
    ownership.
-   Do not enter sensitive personal information into descriptions.
-   For a real deployment, access control, privacy, data retention,
    backups, validation, and secure handling of contact details would
    need to be designed.
-   A real campus lost-and-found service should provide a safe process
    for verifying ownership and returning valuable items.

## 19. Definition of Done

A team has completed the workshop project when it can:

1.  Run the application successfully.
2.  Create both lost and found reports.
3.  Search and display reports.
4.  Mark a report as recovered.
5.  Demonstrate that data persists after restarting.
6.  Explain the role of each module.
7.  Show at least one Git commit or contribution from team members.
8.  Demonstrate the application and describe one test case.

------------------------------------------------------------------------

## Final Workshop Message

> You already know enough Python to start building real software. Start
> with a problem, break it into parts, build together, and test what you
> make.

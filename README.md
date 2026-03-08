# leave-management-automation
***Problem Statement***

Many organizations manage employee leave requests using manual processes such as email submissions or spreadsheet tracking. These approaches create several operational challenges, including:
  - Lack of centralized visibility of leave requests
  - Errors in calculating leave days due to weekends and public holidays
  - Manual tracking of employee leave balances
  - Delayed approval cycles
  - Risk of inaccurate or outdated leave records

Additionally, HR teams often struggle to ensure that employees do not exceed their available leave entitlement because balances are updated manually.

To address these issues, an automated and centralized leave management system was required to streamline request submission, validation, approval, and leave balance management.

***Business Requirements***

The system needed to satisfy the following operational requirements:
  - Employees must be able to submit leave requests through a user-friendly interface.
  - The system must calculate the number of leave days automatically based on the selected start and end dates.
  - Weekends and public holidays must be excluded from the leave duration calculation.
  - The system must verify the employee's available leave balance before approval.
  - Leave requests should follow an approval workflow involving designated managers.
  - Once a request is approved, the approved leave days must automatically be deducted from the employee’s leave balance.
  - All leave records must be stored centrally and accessible for reporting and auditing.
  - HR and administrators must have visibility into leave requests and balances.

***Solution Architecture***

The solution was built using Microsoft Power Platform components integrated with SharePoint and Excel Online.

**Components**

**Power Apps**

Provides the user interface for employees to submit leave requests.
  - Captures leave details such as:
  - Employee information
  - Leave type
  - Start date
  - End date
  - Reason for leave.

SharePoint
  - Stores the Leave Request list, which acts as the primary data repository for submitted requests.
  - Provides structured data storage and integration with Power Automate.

**Excel Online (SharePoint Document Library)**
Two Excel files are maintained:
  1. Public Holiday Calendar
    - Stores official holidays used to exclude non-working days.

  2. Employee Leave Balance
    - Contains employee leave entitlements and remaining balances.

Power Automate
  - Handles the workflow automation, validation logic, and leave balance updates.

***Power Automate Logic (high-level)***

The Power Automate workflow performs the following steps:

Trigger
  - The flow is triggered when a new leave request is submitted via the SharePoint list.

Retrieve Leave Request Data
  - Extract employee information, start date, and end date from the request.

Calculate Leave Duration
  - Determine the total number of days between the start and end dates.
  - Exclude:
    - Weekends
    - Public holidays retrieved from the holiday Excel file.

Check Leave Balance
  - Query the Employee Leave Balance Excel table stored in SharePoint.
  - Validate whether the employee has sufficient leave entitlement.

Approval Process
  - If the balance is sufficient, the flow sends an approval request to the designated manager.

Post-Approval Processing
  - If approved:
    - Deduct the approved leave days from the employee’s leave balance.
    - Update the Excel leave balance file.
    - Update the leave request status in SharePoint.

Notification
  - Notify the employee of the approval or rejection outcome.

***Security & Permissions***

Security and access control were implemented using Microsoft 365 best practices:

SharePoint Permissions
  - Employees can create leave requests but cannot modify approval fields.
  - HR and administrators have full access to the leave management lists.
Excel File Access
  - The leave balance and public holiday files are stored in a secure SharePoint document library.
  - Access is restricted to HR administrators and the automation service account.

Power Automate Connections
  - The workflow runs under controlled credentials to ensure secure access to SharePoint and Excel resources.

Role-Based Access
  - Managers can only approve requests for employees within their reporting structure.

***Outcome / Benefits***

The automation delivered several measurable improvements:

Operational Efficiency
  - Eliminated manual leave calculations and spreadsheet updates.

Accurate Leave Calculations
  - Automatically excludes weekends and public holidays, ensuring correct leave duration.

Improved Approval Speed
  - Automated approval notifications significantly reduced processing time.

Data Accuracy
  - Leave balances are updated automatically, reducing the risk of human error.

Centralized Records
  - All leave requests are stored in SharePoint, enabling easy tracking and reporting.

Scalability
  - The system can easily support additional departments or policy changes.

# Falcon General Ledger (Custom Odoo Module)

## Overview
The **Falcon General Ledger** is a custom Odoo 18 module that provides an interactive and dynamic general ledger report.  
It is built using Odoo’s **Owl framework** and integrates features like:
- Dynamic month-based filtering
- Custom client action with registry integration
- PDF export with `jspdf` and `jspdf-autotable`
- Calendar navigation with dynamic month headers
- Custom menu entry under **Accounting → Falcon Reports**


## Features
-  **Dynamic Calendar Navigation**  
  Users can select a month to automatically refresh the ledger entries and update the header.

-  **Dynamic General Ledger Table**  
  Journal items are fetched dynamically for the selected month.

-  **PDF Export**  
  Generate ledger reports in PDF format using `jspdf` & `jspdf-autotable`.

-  **Seamless Odoo Integration**  
  Uses `ir.actions.client` with a custom action tag (`falcon_general_ledger_tag`).

-  **Extensible OWL Component**  
  Built with Owl Components, easily customizable.

##  Module Structure
custom_general_ledger/
│
├── __manifest__.py
|── __init__.py
├── models/
│ └── __init__.py
├── static/
│ └── src/
│ ├── js/
│ │ └── general_ledger.js # OWL Component + registry action
│ └── xml/
│ └── general_ledger.xml # QWeb template
├── views/
│ └── menus.xml # Menu + Action definitions
| └── templates.xml
  └── views.xml
└── README.md

## Installation

1. Clone this repo inside your Odoo `addons` directory:
   ```bash
   cd /path/to/odoo/custom/addons
   git clone https://github.com/<your-username>/custom_general_ledger.git

2. Update your Odoo config to include the custom addons path if not already set:
addons_path = /path/to/odoo/addons,/path/to/odoo/custom/addons

3. Restart your Odoo server:
./odoo-bin -c odoo.conf -d <your_db> -u custom_general_ledger

4.Activate Developer Mode in Odoo and check under:
 Accounting → Falcon Reports → Falcon General Ledger

**Usage**:
Navigate to Accounting → Falcon Reports → Falcon General Ledger.
Click the Calendar Button to select a month.
The ledger header updates dynamically with the selected month name.
Journal items for that month are fetched and rendered in the table.
Click Export PDF to generate a downloadable PDF report.

**Technical Details:**
Client Action Registration
Registered via the Odoo JS Registry:
registry.category("actions").add("falcon_general_ledger_tag", FalconGeneralLedger);
Assets Loading (from __manifest__.py)
"assets": {
    "web.assets_backend": [
        "custom_general_ledger/static/src/js/general_ledger.js",
    ],
    "web.assets_qweb": [
        "custom_general_ledger/static/src/xml/general_ledger.xml",
    ],
},

**Dependencies**
account (for journal items & financial reports)
jspdf and jspdf-autotable (bundled via Odoo web modules)

**Troubleshooting**
Error: Cannot find key "falcon_general_ledger_tag" in the "actions" registry
Ensure general_ledger.js has /** @odoo-module **/ at the top.

**Rebuild assets:**
./odoo-bin -u custom_general_ledger -d <your_db> --dev=all
Hard refresh browser (Ctrl+Shift+R).
**JS not loading?**
Verify __manifest__.py has correct asset paths.
Check console:
odoo.__DEBUG__.services["registry"].category("actions").keys()

**Contribution:**
Fork the repo
Create a feature branch (git checkout -b feature/new-stuff)
Commit changes (git commit -m 'Add new feature')
Push (git push origin feature/new-stuff)
Open a Pull Request 

**License**
This module is licensed under the MIT License.

# Gspread-
Google Spreadsheets API + Python

Manage your spreadsheets with gspread in Python.
Features:

Open a spreadsheet by its title or url.
Extract range, entire row or column values.
Independent of Google Data Python client library.
Python 3 support.

Basic Usage

Obtain OAuth2 credentials from Google Developers Console

Start using gspread:

import gspread

gc = gspread.authorize(credentials)

# Open a worksheet from spreadsheet with one shot
wks = gc.open("Where is the money Lebowski?").sheet1

wks.update_acell('B2', "it's down there somewhere, let me take another look.")

# Fetch a cell range
cell_list = wks.range('A1:B7')
More Examples

Opening a Spreadsheet

# You can open a spreadsheet by its title as it appears in Google Docs
sh = gc.open('My poor gym results') # <-- Look ma, no keys!

# If you want to be specific, use a key (which can be extracted from
# the spreadsheet's url)
sht1 = gc.open_by_key('0BmgG6nO_6dprdS1MN3d3MkdPa142WFRrdnRRUWl1UFE')

# Or, if you feel really lazy to extract that key, paste the entire url
sht2 = gc.open_by_url('https://docs.google.com/spreadsheet/ccc?key=0Bm...FE&hl')
Creating a Spreadsheet

sh = gc.create('A new spreadsheet')

# But that new spreadsheet will be visible only to your script's account.
# To be able to access newly created spreadsheet you *must* share it
# with your email. Which brings us to…
Sharing a Spreadsheet

sh.share('otto@example.com', perm_type='user', role='writer')
Selecting a Worksheet

# Select worksheet by index. Worksheet indexes start from zero
worksheet = sh.get_worksheet(0)

# By title
worksheet = sh.worksheet("January")

# Most common case: Sheet1
worksheet = sh.sheet1

# Get a list of all worksheets
worksheet_list = sh.worksheets()
Creating a Worksheet

worksheet = sh.add_worksheet(title="A worksheet", rows="100", cols="20")
Deleting a Worksheet

sh.del_worksheet(worksheet)
Getting a Cell Value

# With label
val = worksheet.acell('B1').value

# With coords
val = worksheet.cell(1, 2).value

# To get a cell formula
cell = worksheet.acell('B1') # or .cell(1, 2)
cell.input_value
Getting All Values From a Row or a Column

# Get all values from the first row
values_list = worksheet.row_values(1)

# Get all values from the first column
values_list = worksheet.col_values(1)
Getting All Values From a Worksheet as a List of Lists

list_of_lists = worksheet.get_all_values()
Finding a Cell

# Find a cell with exact string value
cell = worksheet.find("Dough")

print("Found something at R%sC%s" % (cell.row, cell.col))

# Find a cell matching a regular expression
amount_re = re.compile(r'(Big|Enormous) dough')
cell = worksheet.find(amount_re)
Finding All Matched Cells

# Find all cells with string value
cell_list = worksheet.findall("Rug store")

# Find all cells with regexp
criteria_re = re.compile(r'(Small|Room-tiering) rug')
cell_list = worksheet.findall(criteria_re)
Cell Object

Each cell has a value and coordinates properties.

value = cell.value
row_number = cell.row
column_number = cell.col
Updating Cells

worksheet.update_acell('B1', 'Bingo!')

# Or
worksheet.update_cell(1, 2, 'Bingo!')

# Select a range
cell_list = worksheet.range('A1:C7')

for cell in cell_list:
    cell.value = 'O_o'

# Update in batch
worksheet.update_cells(cell_list)
Installation

Requirements

Python 2.6+ or Python 3+

From PyPI

pip install gspread
From GitHub

git clone https://github.com/burnash/gspread.git
cd gspread
python setup.py install

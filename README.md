# Copyright (c) 2026, Shubham Kasar and contributors
# For license information, please see license.txt

import frappe


def execute(filters=None):
	columns = get_columns()
	data = get_data(filters)
	return columns, data

def get_columns():
	return [
		{
			"label":"Student Name",
			"fieldname":"name",
			"fieldtype":"Data",
			"width":200
		},
		{
			"label": "Age",
			"fieldname": "age",
			"fieldtype":"Int",
			"width":100
		}
	]

def get_data(filters):
	conditions = ""

	if filters.get("student"):
		conditions += " AND name = %(student)s"

	if filters.get("age"):
		conditions += " AND age = %(age)s"

	data = frappe.db.sql(f"""SELECT name, age FROM `tabstudent` WHERE 1=1 {conditions}""", filters, as_dict=True)

	return data


---------------------
// JS starts here

// Copyright (c) 2026, Shubham Kasar and contributors
// For license information, please see license.txt

frappe.query_reports["Student script report"] = {
	"filters": [
	{
		"fieldname":"name",
		"label": __("student"),
		"fieldtype":"Link",
		"options":"student"
	},
	{
		"fieldname":"age",
		"label":__("Age"),
		"fieldtype":"Int"
	}
	]
};


  

import sys
import csv
import json
import xml.etree.ElementTree as ET


def convert_to_csv(data, output_file):
    with open(output_file, 'w', newline='', encoding='utf-8') as csv_file:
        writer = csv.writer(csv_file)
        for row in data:
            writer.writerow(row)


def convert_to_json(data, output_file):
    with open(output_file, 'w', encoding='utf-8') as json_file:
        json.dump(data, json_file, indent=4)


def convert_to_xml(data, output_file):
    root = ET.Element("Root")
    for row in data:
        row_element = ET.SubElement(root, "Row")
        for index, cell in enumerate(row):
            cell_element = ET.SubElement(row_element, f"Cell{index}")
            cell_element.text = cell
    tree = ET.ElementTree(root)
    tree.write(output_file)


def main():
    if len(sys.argv) != 3:
        print("Usage: python script.py <filename> <-c|-j|-x>")
        return
    
    filename = sys.argv[1]
    option = sys.argv[2]
    
    try:
        with open(filename, 'r', encoding='windows-1252') as file:
            data = [line.strip().split('\t') for line in file.readlines()]
    except FileNotFoundError:
        print(f"File {filename} not found.")
        return

    if option == '-c':
        convert_to_csv(data, 'output.csv')
        print("File converted to CSV format and saved as 'output.csv'.")
    elif option == '-j':
        convert_to_json(data, 'output.json')
        print("File converted to JSON format and saved as 'output.json'.")
    elif option == '-x':
        convert_to_xml(data, 'output.xml')
        print("File converted to XML format and saved as 'output.xml'.")
    else:
        print("Invalid option. Use -c for CSV, -j for JSON, or -x for XML.")


if __name__ == "__main__":
    main()

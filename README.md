# Project


import xml.etree.ElementTree as ET
import pandas as pd

# Parse XML file
tree = ET.parse("file.xml")  # Replace with your XML file path
root = tree.getroot()

# Extract data
data = []
for service in root.findall("service"):
    uri = service.get("uri")  # Extract attribute value
    route_url = service.find("routeUrl").text if service.find("routeUrl") is not None else ""
    data.append([uri, route_url])

# Convert to DataFrame
df = pd.DataFrame(data, columns=["Service URI", "Route URL"])

# Save to Excel
df.to_excel("output.xlsx", index=False)

print("Data extracted and saved to output.xlsx")

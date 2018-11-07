---
published: true
---
## Creating a CSV file using static data
```
class CSVHelper
{
    public function arrayToCSVFileSaver($data, $fields, $filename, $delimiter = ";", $enclosure = '"')
    {
        // Open the file $filename for writing
        $file = fopen($filename, 'w');
        // Save the column headers
        fputcsv($file, $fields, $delimiter, $enclosure);
        // Save each row of the data
        foreach ($data as $row) {
            fputcsv($file, $row, $delimiter, $enclosure);
        }
        // Close the file
        fclose($file);
    }

}
```

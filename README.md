# React Excel File Data Fetcher

This project allows you to fetch data from an Excel file and display it in a React component.

![image](https://github.com/lexzer42/fetch-data-from-excel-file/assets/134535937/cdb1bc52-1330-446b-92b1-b0c1eac7367e)

## Getting Started

Follow these steps to set up the project:

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/your-repository.git
   ```

2. Navigate to the project directory:
   ```
   cd your-repository
   ```

3. Install dependencies:
   ```
   npm install
   ```

1. Install the required dependencies using npm or yarn:
   ```
   npm install xlsx
   ```

2. Import the necessary dependencies in your React component:
   ```javascript
   import React, { useState } from 'react';
   import * as XLSX from 'xlsx';
   ```

3. Set up state to store the Excel data:
   ```javascript
   const [data, setData] = useState([]);
   ```

4. Create an input element of type "file" to allow users to choose an Excel file.

5. Define a function to handle file upload and process the selected file:
   ```javascript
   const handleFileUpload = (e) => {
     const file = e.target.files[0];
     const reader = new FileReader();
     reader.onload = (event) => {
       const binaryString = event.target.result;
       const workbook = XLSX.read(binaryString, { type: 'binary' });
       const sheetName = workbook.SheetNames[0];
       const sheet = workbook.Sheets[sheetName];
       const jsonData = XLSX.utils.sheet_to_json(sheet);
       setData(jsonData);
     };
     reader.readAsBinaryString(file);
   };
   ```

6. Check if the data is not empty and display it in a table:
   ```javascript
   return (
     <div>
       <input type="file" onChange={handleFileUpload} />
       {data.length > 0 && (
         <table>
           <thead>
             <tr>
               {Object.keys(data[0]).map((key) => (
                 <th key={key}>{key}</th>
               ))}
             </tr>
           </thead>
           <tbody>
             {data.map((row, index) => (
               <tr key={index}>
                 {Object.values(row).map((value, index) => (
                   <td key={index}>{value}</td>
                 ))}
               </tr>
             ))}
           </tbody>
         </table>
       )}
     </div>
   );
   ```

Now, when you upload an Excel file, the data will be displayed in a table.

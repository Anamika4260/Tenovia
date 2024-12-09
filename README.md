# Tenovia
Database Schema 

## Inventory Management System Report

### Objective
Develop a lightweight inventory management tool to track stock levels, optimize supply chain workflows, and minimize out-of-stock scenarios.

### Key Components

1. **Database Schema:**
   - A PostgreSQL database schema to store inventory details was created. The schema includes the following fields:
     ```sql
     CREATE TABLE Products (
         ProductID SERIAL PRIMARY KEY,
         ProductName VARCHAR(255) NOT NULL,
         StockLevel INT NOT NULL,
         ReorderLevel INT NOT NULL CHECK (ReorderLevel >= 0),
         CreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP
     );
     ```

2. **API Implementation:**
   - RESTful APIs were implemented using Node.js with Express for stock management. The following key endpoints were created:
     - **GET /api/products**: Retrieve all products
     - **POST /api/products**: Add a new product
     - **PUT /api/products/:id**: Update stock level for a product
     - **DELETE /api/products/:id**: Delete a product from the inventory

   - **Sample code snippet for API implementation:**
   ```javascript
   const express = require('express');
   const { Pool } = require('pg');
   const app = express();
   
   app.use(express.json());
   const pool = new Pool({ /* database configuration */ });

   app.get('/api/products', async (req, res) => {
       // Retrieve all products logic
   });
   app.post('/api/products', async (req, res) => {
       // Add new product logic
   });
   // Other endpoints...
   ```

3. **Frontend Development:**
   - A simple frontend application was built using React to visualize the inventory status.
   - The key component displays a list of products along with their stock levels and provides functionality to add and update products.

   - **Sample code snippet for Frontend:**
   ```jsx
   import React, { useEffect, useState } from 'react';
   import axios from 'axios';

   const InventoryApp = () => {
       const [inventory, setInventory] = useState([]);

       useEffect(() => {
           const fetchInventory = async () => {
               const result = await axios.get('/api/products');
               setInventory(result.data);
           };
           fetchInventory();
       }, []);

       return (
           <div>
               <h1>Inventory Management</h1>
               <ul>
                   {inventory.map(item => (
                       <li key={item.ProductID}>{item.ProductName}: {item.StockLevel}</li>
                   ))}
               </ul>
           </div>
       );
   };

   export default InventoryApp;
   ```

4. **Analytics Integration:**
   - Basic analytics were integrated to identify "Top Products at Risk of Stock Out" by filtering products where the stock level is less than or equal to the reorder level.

   - **Sample analytics function:**
   ```javascript
   const getAtRiskProducts = (inventory) => {
       return inventory.filter(item => item.StockLevel <= item.ReorderLevel);
   };
   ```

### Deliverables
- A complete codebase hosted in a GitHub repository, containing:
  - Database schema
  - API code and documentation
  - Frontend code
- A presentation summarizing the approach taken, challenges encountered, and the outcomes achieved in the development of the inventory management system.

### Conclusion
This report outlines the structure and implementation of a lightweight inventory management system designed to efficiently track stock levels, optimize workflows, and reduce the chances of stock outs. The system is built using a modern tech stack, ensuring scalability and performance.



# Web Scraping from TrueCar

web scraping from **Truecar** site  and Transfer to mysql database:

![photo_۲۰۲۳-۰۸-۰۷_۱۲-۰۷-۲۱](https://github.com/Peyman2012/web-scraping-from-truecar-site-/assets/88220773/f6a2eb6a-ba5c-428f-ad3f-95bc647b3304)

---

## **Project Description**
This project is a **web scraping script** that extracts used car information from the [TrueCar](https://www.truecar.com/used-cars-for-sale/listings/?buyOnline=true) website. The extracted data includes:
- **Car Name**
- **Mileage**
- **Original Price (Before Discount)**
- **Discount Amount**
- **Final Price (After Discount)**

The collected data is stored in a **CSV file** and also uploaded to a **MySQL database**.

---
## **Prerequisites**
Before running the script, ensure you have installed the following dependencies:
```bash
pip install requests beautifulsoup4 pandas mysql-connector-python
```
You also need **MySQL** installed on your system. Make sure MySQL is running and that you have a user with the necessary permissions.

---
## **How to Run**

### 1. **Execute the Script and Collect Data**
Run the `web_scraping.py` file:
```bash
python web_scraping.py
```
This script retrieves data from TrueCar and saves it in a `Buy_Price.csv` file.

### 2. **Store Data in the Database**
Ensure **MySQL is running**, and the data will be stored in the `buy_car` database.

---
## **Key Code Sections**

### **1. Fetching Web Content**
```python
url = 'https://www.truecar.com/used-cars-for-sale/listings/?buyOnline=true'
res = requests.get(url)
soup = BeautifulSoup(res.text, 'html.parser')
```
Retrieves the TrueCar webpage and parses it using **BeautifulSoup**.

### **2. Extracting Data**
Car name, mileage, prices, and discounts are extracted from the HTML page:
```python
machin_name = soup.find_all('div', attrs={'class': 'vehicle-card-top'})
machin_miles = soup.find_all('div', attrs={'class': 'mt-2-5 w-full border-t pt-2-5'})
machin_price = soup.find_all('div', attrs={'class': 'text-sm line-through'})
machin_takhfif = soup.find_all('div', attrs={'class': 'heading-3 font-bold'})
```

### **3. Saving Data to CSV**
```python
df = pd.DataFrame({'Name_Car': name_car, 'Miles': Miles, 'Discount': Discount, 'With_Discount': with_discount, 'Purchase_price': Purchase_price})
df.to_csv('Buy_Price.csv', index=False)
```

### **4. Storing Data in MySQL**
```python
con = msql.connect(host='127.0.0.1', user='root', password='', database='buy_car')
cursor = con.cursor()
cursor.execute("INSERT INTO buy_price_car VALUES (%s, %s, %s, %s, %s)", tuple(row))
con.commit()
```

---
## **Common Issues and Solutions**
| Issue | Solution |
|-----------------|-------------------------------------------------|
| TrueCar blocks requests | Use a fake User-Agent or **Proxies** |
| HTML structure changes | Check **XPath or the site’s API** |
| MySQL connection error | Ensure MySQL is running and you have access |

---
## **Suggested Improvements**
✅ **Use Selenium for dynamic websites**<br>
✅ **Use a User-Agent to avoid blocking**<br>
✅ **Implement an ORM like SQLAlchemy for database management**<br>
✅ **Optimize data storage in JSON or MongoDB**

---
Output in mysql database:

![photo_۲۰۲۳-۰۸-۰۷_۱۷-۰۷-۴۲](https://github.com/Peyman2012/web-scraping-from-truecar-site-/assets/88220773/b67e3899-ad2c-4f98-a4e1-5950bdaad8cf)

output 3 from project 3 :

![photo_2023-08-12_17-24-39](https://github.com/Peyman2012/web-scraping-from-truecar-site-/assets/88220773/17defbc7-59a6-4f33-abde-a063e60de31c)
---
## **License**
This project is released under the **MIT License**. You are free to use, modify, and share it.

---
### **Author:**
🚀 Developer: **[Peyman Daei Rezaei]**

📧 Email: peimandaii2012@gmail.com









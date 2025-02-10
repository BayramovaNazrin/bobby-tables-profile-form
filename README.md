# Bobby Tables Profile Form

## 📝 Description
This project demonstrates secure user input handling in PHP for a profile creation form. It validates user inputs to prevent security vulnerabilities, inspired by the **Bobby Tables** comic.

## 🚀 Installation
1. Clone the repository:  
   ```bash
   git clone https://github.com/BayramovaNazrin/bobby-tables-profile-form.git

## 📌 Usage
- Fill out the profile form with user details.  
- Submit the form to see input validation in action.  

## 🛠️ Technologies Used
- **PHP**  
- **HTML**  

## 🔒 Features
- ✅ **HTML entity conversion** to prevent XSS attacks.  
- ✅ **Trims unnecessary whitespaces** from user input.  
- ✅ **Checks if the username already exists** to prevent impersonation.  
- ✅ **Validates characters** to ensure proper formatting.  
- ✅ **Email format validation** to reject invalid emails.  
- ✅ **Birth year range validation** to allow only valid years.


## 📜 Code Snippets

### **1. Preventing XSS Attacks & Whitespace Handling**
```php
$raw_name = trim(htmlspecialchars($_POST["name"]));
```
✅ `htmlspecialchars()` converts HTML characters to entities, preventing XSS.
✅ `trim()` removes leading and trailing whitespaces.

---

### **2. Preventing Username Impersonation**
```php
if (in_array($raw_name, $existing_users)) {
    $validation_error .= "This name is taken. <br> ";
} else {
    $raw_name = lcfirst($raw_name);
    $name = $raw_name;
}
```
✅ `in_array()` checks if the username already exists.
✅ Ensures names start with a lowercase letter.

---

### **3. Validating Character Selection**
```php
if (in_array($raw_character, ["wizard","mage", "orc"])) {
    if ($raw_character == "mage") {
        if (isMage($raw_birth_year)) {
            echo "real talent";
            $character = $raw_character;
        } else {
            echo "sorry. you can not be a mage";
        }
    } else {
        $character = $raw_character;
    }
} else {
    $validation_error .= "You must pick a wizard, mage or orc. <br>";
}
```
✅ `in_array()` ensures only valid characters are allowed.
✅ Implements a special rule where **mages must be born in leap years**.

---

### **4. Validating Email Format**
```php
if (filter_var($raw_email, FILTER_VALIDATE_EMAIL)) {
    if (strrchr($raw_email,".com") == ".com") {
        $email = $raw_email;
    }
} else {
    $validation_error .= "Invalid email. <br>";
}
```
✅ `filter_var()` ensures the input is a valid email.
✅ `strrchr()` checks if the email ends in ".com".

---

### **5. Ensuring Birth Year is Valid**
```php
$options = ["options" => ["min_range" => 1900, "max_range" => date("Y")]];
if (filter_var($raw_birth_year, FILTER_VALIDATE_INT, $options)) {
    $birth_year = $raw_birth_year;
} else {
    $validation_error .= "That can't be your birth year. <br>";
}
```
✅ Ensures birth year is between 1900 and the current year.
✅ `filter_var()` ensures only valid integer inputs.

---

## ⚔️ Challenges and Solutions

### **1. Allowing HTML characters in Names Without Executing Code**
**Challenge:** Users could input `<h1>HELLO</h1>`, which could manipulate page structure.
**Solution:** Used `htmlspecialchars()` to escape HTML characters.

### **2. Ensuring Users Select Only Allowed Character Types**
**Challenge:** Users could manipulate the HTML and select invalid character types.
**Solution:** Used `in_array()` to restrict input to "wizard", "mage", or "orc".

### **3. Validating Mages’ Birth Year (Task 15)**
**Challenge:** Mages should only be born in leap years.
**Solution:**
```php
function isMage($raw_birth_year) {
    return (($raw_birth_year % 4 == 0 && $raw_birth_year % 100 != 0) || ($raw_birth_year % 400 == 0));
}
```
✅ This function checks if a year is a **leap year** using the standard formula.
✅ If a user selects "mage" but their birth year is not a leap year, they receive an error.

---

## 🎉 Conclusion
This form is now **secure** against malicious users. It prevents **XSS**, enforces **input validation**, and adds an interesting logic rule for **mages & leap years**. 🚀


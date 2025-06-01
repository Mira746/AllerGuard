Synapse_2025
📝 Project Report: Food Allergen Detection and Recommendation System
👩‍⚕️ Objective
Design a system to:

Detect potential allergens in meals.
Manage dietary restrictions.
Predict allergy risks.
Suggest safe alternatives.
Group similar food products.
Enhance food safety awareness.
📥 Input Types Supported
Barcode Input

User enters a barcode.
System fetches product name, ingredients, and allergens using an API.
Manual Ingredients Input

User manually enters a list of ingredients.
Image of Ingredients List

User uploads a photo.
Image is processed using OCR (Tesseract via pytesseract) to extract ingredients.
🔌 APIs Integrated
OpenFoodFacts API

Used to fetch ingredients and allergens from barcode.
Endpoint: https://world.openfoodfacts.org/api/v0/product/{barcode}.json
🔍 Features Implemented
1. Allergen Detection (Multi-label Classification)
Input: Ingredients (text)
Output: List of allergens
Model: RandomForestClassifier
Vectorizer: TF-IDF Vectorizer
Evaluation: MultiLabelBinarizer for training labels
2. Risk Level Prediction (Text Classification)
Input: Ingredients
Output: Risk Level (High, Medium, Low)
Model: LogisticRegression or RandomForestClassifier
Vectorizer: TF-IDF Vectorizer
3. Suggest Alternatives (Rule-Based + API)
Input: Detected Allergens

Output: List of safe substitutes

Approach:

If API has results → use API
Else → use predefined rule-based dictionary
4. Clustering Similar Foods (Unsupervised Learning)
Input: Ingredients

Output: Cluster Labels

Technique:

TF-IDF Vectorization
KMeans Clustering
Elbow Method to determine optimal k
🧠 ML Pipeline Overview
Training Data
Dataset Columns: ['Food Name', 'Ingredients', 'Detected Allergens', 'Risk Level', 'Notes', 'Alternative Suggestions']
Preprocessing
Cleaned ingredients and allergen lists.
Applied TF-IDF vectorization.
Converted multi-label targets using MultiLabelBinarizer.
Models Trained
Task	Model Used	Vectorizer
Allergen Detection	RandomForestClassifier	TF-IDF
Risk Level Prediction	LogisticRegression	TF-IDF
Similar Food Clustering	KMeans	TF-IDF
🧪 Sample Workflow (Main Function)
def main():
    input_type = input("Enter input type (barcode/manual/image): ").lower()

    if input_type == "barcode":
        barcode = input("Enter the barcode: ")
        food_name, ingredients, allergens = fetch_data_from_barcode(barcode)
    elif input_type == "manual":
        ingredients = input("Enter the ingredients: ")
    elif input_type == "image":
        image_path = input("Upload image path: ")
        ingredients = extract_ingredients_from_image(image_path)
    else:
        print("Invalid input type.")
        return

    detected_allergens = detect_allergens_from_ingredients(ingredients)
    risk = predict_risk_level(ingredients)
    alternatives = suggest_alternatives(detected_allergens)

    print("Ingredients:", ingredients)
    print("Detected Allergens:", detected_allergens)
    print("Risk Level:", risk)
    print("Suggested Alternatives:", alternatives)
📚 Libraries & Tools Used
scikit-learn
pandas, numpy
pytesseract, Pillow
requests, json
matplotlib (for elbow method)
google.colab (for file uploads)
✅ Outcomes
Successfully trained models for risk and allergen detection.
Integrated barcode scanning and image-to-text OCR.
Rule-based and API-backed alternative suggestion system.
Clustering model groups similar food items for better navigation.
👩‍🔬 Group Members:-

Komal Sikchi

Mira Vadjikar

Nidhi Borkar

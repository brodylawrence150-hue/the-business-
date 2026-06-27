# Initialize the Gemini model
gemini_model = genai.GenerativeModel('gemini-pro')

def explain_physics_concept(prompt):
    """
    Uses the Gemini model to explain a physics concept.
    """
    try:
        response = gemini_model.generate_content(f"Explain the following physics concept for a student, including how it relates to Earth or other natural phenomena: {prompt}")
        return response.text
    except Exception as e:
        return f"Sorry, I encountered an error: {e}\nPlease ensure your GOOGLE_API_KEY is correctly set in Colab secrets and the Gemini API is configured."

# Example usage: Ask about gravity
concept_to_explain = "gravity"
explanation = explain_physics_concept(concept_to_explain)
print(f"### Explanation of {concept_to_explain.capitalize()}:\n")
print(explanation)

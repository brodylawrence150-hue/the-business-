import streamlit as st

# Initialize session state for expenses if not already present
if 'expense_categories' not in st.session_state:
    st.session_state.expense_categories = {
        'Food': 0,
        'Transportation': 0,
        'Utilities': 0,
        'Supplies': 0,
        'Marketing': 0,
        'Rent': 0,
        'Miscellaneous': 0
    }
if 'transactions' not in st.session_state:
    st.session_state.transactions = []

def categorize_expense_web(item, selected_category=None):
    item_lower = item.lower()
    if selected_category:
        return selected_category
    # Existing categorization logic as a fallback or for initial suggestions
    if 'coffee' in item_lower or 'lunch' in item_lower or 'dinner' in item_lower or 'groceries' in item_lower:
        return 'Food'
    elif 'gas' in item_lower or 'fuel' in item_lower or 'bus' in item_lower or 'taxi' in item_lower or 'uber' in item_lower:
        return 'Transportation'
    elif 'electricity' in item_lower or 'water' in item_lower or 'internet' in item_lower or 'phone' in item_lower:
        return 'Utilities'
    elif 'paper' in item_lower or 'pen' in item_lower or 'ink' in item_lower or 'office' in item_lower:
        return 'Supplies'
    elif 'ad' in item_lower or 'social media' in item_lower or 'promotion' in item_lower:
        return 'Marketing'
    elif 'rent' in item_lower:
        return 'Rent'
    else:
        return 'Miscellaneous'

# Streamlit app layout
st.set_page_config(layout='wide')
st.title('📊 Simple Expense Categorizer Web App')

st.markdown("""
This application helps you categorize and track your expenses. 
Input your expense details, select a category, and add it to the ledger.
""")

# Input fields
with st.form(key='expense_form'):
    st.header('Add New Expense')
    expense_item = st.text_input('Expense Item', placeholder='e.g., Coffee, Bus fare, Office Supplies')
    expense_amount = st.number_input('Amount', min_value=0.0, format='%.2f')
    
    # Dropdown for categories
    category_options = list(st.session_state.expense_categories.keys())
    selected_category = st.selectbox('Select Category', options=category_options)

    add_expense_button = st.form_submit_button('Add Expense')

    if add_expense_button:
        if expense_item and expense_amount > 0:
            # Use the selected category from the dropdown
            category = categorize_expense_web(expense_item, selected_category=selected_category)
            
            st.session_state.expense_categories[category] += expense_amount
            st.session_state.transactions.append({'Item': expense_item, 'Amount': expense_amount, 'Category': category})
            st.success(f"'{expense_item}' (${expense_amount:.2f}) categorized as '{category}'.")
        else:
            st.error("Please enter a valid expense item and a positive amount.")

st.markdown('---')

st.header('💰 All Expenses')
if st.session_state.transactions:
    # Display transactions in a DataFrame
    transactions_df = pd.DataFrame(st.session_state.transactions)
    st.dataframe(transactions_df, use_container_width=True)
else:
    st.info('No expenses added yet. Use the form above to add your first expense!')

st.markdown('---')

st.header('📈 Expense Summary')
if any(st.session_state.expense_categories.values()):
    summary_data = [{'Category': cat, 'Total Amount': f'${amount:.2f}'} for cat, amount in st.session_state.expense_categories.items()]
    summary_df = pd.DataFrame(summary_data)
    st.table(summary_df) # Using st.table for a cleaner, official-looking summary

    total_all_expenses = sum(st.session_state.expense_categories.values())
    st.metric(label="Total All Expenses", value=f"${total_all_expenses:.2f}")
else:
    st.info('No expenses to summarize yet.')

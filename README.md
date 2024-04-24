# bmac-paywall
creates a buymeacoffee paywall for streamlit apps
# BMAC Paywall for Streamlit Apps

This repository contains the necessary code to integrate a BuyMeACoffee (BMAC) paywall with Streamlit apps. This system allows for access control to your apps based on BMAC subscriber status associated with specific membership plans.

## How It Works

The system utilizes the BMAC API to fetch all active subscribers and checks whether a user's email corresponds to a subscription with a specified membership ID. Access to the app is granted only if the user's subscription matches this hardcoded membership ID.

## Repository Files

### `authentication.py`
This module is pivotal and includes two primary functions:
- **fetch_subscribers**: This function connects to the BMAC API and retrieves a list of all current subscribers.
- **is_subscriber_authorized**: This function checks if a particular email is associated with a subscriber who has the correct membership level.

## Usage

To integrate this paywall system into a new Streamlit app, follow these steps:

1. **Clone this Repository**
   - Clone or download this repository into your project directory where your Streamlit app resides.

2. **Set Up BMAC API Key**
   - Securely store your BMAC API key in Streamlit’s secrets management under the key `bmac_api_key`.

3. **Import Functions**
   - Import the necessary functions from `authentication.py` into your main Streamlit app script.

4. **Modify Membership Level ID**
   - Update the `membership_level_id` in the `is_subscriber_authorized` function to correspond to the ID for the plan that should have access to your app.

### Modifying Membership Level ID

Modify the code for different apps by changing the `membership_level_id` in the `is_subscriber_authorized` function to match the appropriate plan:

```python
def is_subscriber_authorized(email, subscribers):
    """
    Update the membership_level_id to match the required plan for your new app.
    """
    target_membership_id = 187451  # Update this ID as needed for different plans
    for subscriber in subscribers:
        if ('payer_email' in subscriber and 'membership_level_id' in subscriber and
            subscriber['payer_email'] == email and subscriber['membership_level_id'] == target_membership_id):
            return True
    return False

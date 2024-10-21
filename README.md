import streamlit as st

# Function to gather business information
def gather_information():
    st.title("Strategic Management Advisor GPT")
    st.write("Welcome! Let’s start by gathering some business information.")
    
    business_name = st.text_input("What is the name of your business?")
    industry = st.text_input("Which industry does your business operate in?")
    competitors = st.text_area("Do you have any data or insights on competitors or market trends?")
    
    if st.button("Proceed to SWOT Analysis"):
        return business_name, industry, competitors
    return None, None, None

# Function to conduct SWOT Analysis
def swot_analysis():
    st.subheader("SWOT Analysis")
    
    strengths = st.text_input("What are your business’s strengths?")
    weaknesses = st.text_input("What are your business’s weaknesses?")
    opportunities = st.text_input("What market opportunities do you see?")
    threats = st.text_input("What threats from competitors or external factors do you face?")
    
    if st.button("Proceed to Porter's Five Forces"):
        return strengths, weaknesses, opportunities, threats
    return None, None, None, None

# Function for Porter's Five Forces analysis
def porters_five_forces():
    st.subheader("Porter’s Five Forces Analysis")
    
    new_entrants = st.radio("Is there a high threat of new entrants?", ('Yes', 'No'))
    supplier_power = st.radio("Do suppliers have strong bargaining power?", ('Yes', 'No'))
    buyer_power = st.radio("Do customers have strong bargaining power?", ('Yes', 'No'))
    substitutes = st.radio("Is there a high threat of substitutes?", ('Yes', 'No'))
    rivalry = st.radio("How intense is rivalry among existing competitors?", ('Low', 'Moderate', 'High'))
    
    if st.button("Generate Strategic Recommendations"):
        return new_entrants, supplier_power, buyer_power, substitutes, rivalry
    return None, None, None, None, None

# Function to provide strategic recommendations
def provide_recommendations(swot_data, porter_data):
    st.subheader("Strategic Recommendations")
    strengths, weaknesses, opportunities, threats = swot_data
    new_entrants, supplier_power, buyer_power, substitutes, rivalry = porter_data
    
    st.write(f"Based on your SWOT analysis:")
    
    if strengths:
        st.write(f"- Leverage strengths like **{strengths}** to gain a competitive advantage in the market.")
    if weaknesses:
        st.write(f"- Address weaknesses such as **{weaknesses}** to strengthen internal operations.")
    if opportunities:
        st.write(f"- Seize opportunities like **{opportunities}** to expand market presence.")
    if threats:
        st.write(f"- Prepare for potential threats such as **{threats}** by implementing mitigation strategies.")
    
    st.write("\nBased on Porter’s Five Forces analysis:")
    
    if new_entrants == 'Yes':
        st.write("- Create barriers to entry to deter new competitors from entering the market.")
    if supplier_power == 'Yes':
        st.write("- Diversify suppliers to reduce their bargaining power.")
    if buyer_power == 'Yes':
        st.write("- Introduce loyalty programs to reduce customer bargaining power.")
    if substitutes == 'Yes':
        st.write("- Differentiate products/services to lower the threat of substitutes.")
    if rivalry == 'High':
        st.write("- Focus on a unique value proposition to stand out in a competitive market.")

# Main function to run the strategic management advisor
def strategic_management_advisor():
    business_name, industry, competitors = gather_information()
    
    if business_name and industry:
        swot_data = swot_analysis()
        if all(swot_data):
            porter_data = porters_five_forces()
            if all(porter_data):
                provide_recommendations(swot_data, porter_data)

# Run the strategic management advisor
if __name__ == '__main__':
    strategic_management_advisor()

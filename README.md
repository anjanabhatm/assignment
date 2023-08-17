# assignment
import streamlit as st
import numpy as np
import pandas as pd

def main():
    st.title("Normal Distribution Generator and Histogram")
    
    st.sidebar.header("Settings")
    
    mean = st.sidebar.number_input("Mean", value=0.0)
    std_dev = st.sidebar.number_input("Standard Deviation", value=1.0)
    num_samples = st.sidebar.number_input("Number of Samples", value=1000, min_value=1)
    
    if st.sidebar.button("Generate Data"):
        data = np.random.normal(mean, std_dev, num_samples)
        df = pd.DataFrame(data, columns=["Value"])
        
        st.subheader("Generated Data")
        st.dataframe(df)
        
        st.subheader("Histogram")
        st.pyplot(histogram_plot(data))
        
        st.sidebar.markdown(get_csv_download_link(df), unsafe_allow_html=True)

def histogram_plot(data):
    import matplotlib.pyplot as plt
    plt.hist(data, bins=20)
    plt.xlabel("Value")
    plt.ylabel("Frequency")
    plt.title("Histogram of Generated Data")
    return plt

def get_csv_download_link(df):
    csv = df.to_csv(index=False)
    b64 = base64.b64encode(csv.encode()).decode()
    return f'<a href="data:file/csv;base64,{b64}" download="generated_data.csv">Download CSV</a>'

if __name__ == "__main__":
    main()

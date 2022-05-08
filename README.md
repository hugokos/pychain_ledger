# pychain_ledger
Python blockchain ledger system with streamlit web interface

## Technologies

Project uses:

[Pandas](https://pandas.pydata.org/)

[DataClasses]https://docs.python.org/3/library/dataclasses.html)

[Typing](https://docs.python.org/3/library/typing.html)

[DateTime](https://docs.python.org/3/library/datetime.html)

[Streamlit](https://docs.streamlit.io/)

[Hashlib](https://docs.python.org/3/library/hashlib.html)

---

## Installation Guide

Run this program in Jupyter notebook and have a Pandas, DataClasses, Typing, Streamlit, Datetime, and Hashlib installed. 



---

## Usage

Utilize terminal to interact with the program. Test the program by storing records when you run the PyChain ledger and user interface by running the Streamlit application and storing some mined blocks in the PyChain ledger. Then test the blockchain validation process by using your PyChain ledger.

!['Screen Shot of Streamlit'](https://github.com/hugokos/pychain_ledger/Streamlit_Screenshot.JPG)



**Key example code for StreamLit**
```
# Add an input area where you can get a value for `sender` from the user.
sender_data = st.text_input("Sender")

# Add an input area where you can get a value for `receiver` from the user.
reciever_data = st.text_input("Reciever")

# Add an input area where you can get a value for `amount` from the user.
amount_data = st.text_input("Amount")

if st.button("Add Block"):
    prev_block = pychain.chain[-1]
    prev_block_hash = prev_block.hash_block()

    # Update `new_block` so that `Block` consists of an attribute named `record`
    # which is set equal to a `Record` that contains the `sender`, `receiver`,
    # and `amount` values
    new_block = Block(
        record=Record(sender_data, reciever_data, amount_data),
        creator_id=42,
        prev_hash=prev_block_hash
    )

    pychain.add_block(new_block)
    st.balloons()


st.markdown("## The PyChain Ledger")

pychain_df = pd.DataFrame(pychain.chain).astype(str)
st.write(pychain_df)

difficulty = st.sidebar.slider("Block Difficulty", 1, 5, 2)
pychain.difficulty = difficulty

st.sidebar.write("# Block Inspector")
selected_block = st.sidebar.selectbox(
    "Which block would you like to see?", pychain.chain
)

st.sidebar.write(selected_block)

if st.button("Validate Chain"):
    st.write(pychain.is_valid())

---

## Contributors

Hugo Kostelni

---

## License

Open Source
'
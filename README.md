# Task-5-Python
contacts = []  # List to store contacts as dictionaries

def add_contact():
  """Prompts user for contact details and adds a new contact."""
  name = input("Enter contact name: ")
  phone_number = input("Enter phone number: ")
  email = input("Enter email (optional): ")
  address = input("Enter address (optional): ")
  contact = {"name": name, "phone_number": phone_number, "email": email, "address": address}
  contacts.append(contact)
  print("Contact added successfully!")

def view_contacts():
  """Displays a list of all contacts with names and phone numbers."""
  if not contacts:
    print("No contacts found.")
  else:
    print("-" * 40)
    print("Contact List:")
    print("-" * 40)
    for i, contact in enumerate(contacts):
      print(f"{i+1}. {contact['name']} - {contact['phone_number']}")
    print("-" * 40)

def search_contact():
  """Searches for contacts by name or phone number."""
  search_term = input("Enter name or phone number to search: ")
  found_contacts = []
  for contact in contacts:
    if search_term.lower() in contact["name"].lower() or search_term in contact["phone_number"]:
      found_contacts.append(contact)
  if found_contacts:
    print("\nSearch Results:")
    print("-" * 40)
    for i, contact in enumerate(found_contacts):
      print(f"{i+1}. {contact['name']} - {contact['phone_number']}")
      if contact["email"]:
        print(f"  Email: {contact['email']}")
      if contact["address"]:
        print(f"  Address: {contact['address']}")
    print("-" * 40)
  else:
    print("No contacts found matching that search term.")

def update_contact():
  """Allows updating details of an existing contact."""
  if not contacts:
    print("No contacts found to update.")
    return
  view_contacts()  # Display list for reference
  index = int(input("Enter the contact number to update (1-" + str(len(contacts)) + "): ")) - 1
  if 0 <= index < len(contacts):
    contact = contacts[index]
    print("Current Details:")
    print(f"  Name: {contact['name']}")
    print(f"  Phone number: {contact['phone_number']}")
    print(f"  Email: {contact['email']}" if contact["email"] else "  Email: Not set")
    print(f"  Address: {contact['address']}" if contact["address"] else "  Address: Not set")
    updated_name = input("Update name (leave blank to keep current): ")
    updated_phone_number = input("Update phone number (leave blank to keep current): ")
    updated_email = input("Update email (leave blank to keep current): ")
    updated_address = input("Update address (leave blank to keep current): ")
    if updated_name:
      contact["name"] = updated_name
    if updated_phone_number:
      contact["phone_number"] = updated_phone_number
    if updated_email:
      contact["email"] = updated_email
    if updated_address:
      contact["address"] = updated_address
    print("Contact updated successfully!")
  else:
    print("Invalid contact number.")

def delete_contact():
  """Allows deleting a contact."""
  if not contacts:
    print("No contacts found to delete.")
    return
  view_contacts()  # Display list for reference
  index = int(input("Enter the contact number to delete (1-" + str(len(contacts)) + "): ")) - 1
  if 0 <= index < len(contacts):
    contacts.pop(index)
    print("Contact deleted successfully!")
  else:
    print("Invalid contact number.")

def main_menu():
  """Displays the main menu and handles user choices."""
  while True:
    print("\nContact Management System")
    print("-" * 40)
    print("1. Add Contact")
    print("2. View Contact List")
    print("3. Search Contact")

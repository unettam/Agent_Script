# Agent_Script
#Scripting for Neoleon IT Services 

import os
import glob
import time

# Function to read the files and extract content
def read_files(file_paths):
    content = ""
    for file_path in file_paths:
        with open(file_path, 'r') as file:
            content += file.read() + "\n"
    return content

# Function to generate a default answer
def generate_default_answer():
    return "I'm sorry, I don't have the information to answer that question at the moment."

# Function to create an agent
def create_agent():
    agent = {
        "files": [],
        "knowledge": ""
    }
    return agent

# Function to ask a question to the agent
def ask_question(agent, question):
    if not agent["knowledge"]:
        return generate_default_answer()

    # Process the question using the agent's knowledge
    # You can use any NLP technique or library here to analyze the question and find relevant information from the files

    # Placeholder logic - check if the question appears in the agent's knowledge
    if question in agent["knowledge"]:
        return "The answer to your question is: ... (extracted from the files)"
    else:
        return generate_default_answer()

# Function to upload files to the agent
def upload_files(agent, file_paths):
    agent["files"].extend(file_paths)
    agent["knowledge"] = read_files(agent["files"])

# Main script
def main():
    agent = create_agent()

    # User interaction loop
    while True:
        user_input = input("Enter your question or type 'upload' to provide files: ")

        if user_input.lower() == "upload":
            file_paths = []
            files_folder = input("Enter the folder path where your files are located: ")
            file_extension = input("Enter the file extension (e.g., txt): ")

            # Find files with the specified extension in the folder
            file_paths = glob.glob(os.path.join(files_folder, f"*.{file_extension}"))

            if len(file_paths) == 0:
                print("No files found.")
            else:
                upload_files(agent, file_paths)
                print("Files uploaded successfully.")

        else:
            answer = ask_question(agent, user_input)
            print("Agent:", answer)

        time.sleep(1)  # Delay between interactions

if __name__ == "__main__":
    main()

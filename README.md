# File-Manager
import os
import shutil

def organize_files(directory):
    categories = {
        'Images': ['.jpg', '.jpeg', '.png', '.gif', '.bmp', '.tiff'],
        'Documents': ['.pdf', '.doc', '.docx', '.txt', '.xls', '.xlsx', '.ppt', '.pptx'],
        'Videos': ['.mp4', '.mkv', '.avi', '.mov', '.flv'],
        'Others': []
    }

    for filename in os.listdir(directory):
        file_path = os.path.join(directory, filename)

        if os.path.isdir(file_path):
            continue

        file_extension = os.path.splitext(filename)[1].lower()
        moved = False

        for category, extensions in categories.items():
            if file_extension in extensions:
                target_dir = os.path.join(directory, category)
                os.makedirs(target_dir, exist_ok=True)
                shutil.move(file_path, os.path.join(target_dir, filename))
                print(f"Moving {file_path} to {os.path.join(target_dir, filename)}")
                moved = True
                break

        if not moved:
            target_dir = os.path.join(directory, 'Others')
            os.makedirs(target_dir, exist_ok=True)
            shutil.move(file_path, os.path.join(target_dir, filename))
            print(f"Moving {file_path} to {os.path.join(target_dir, filename)}")

    print(f"Files organized in: {directory}")

directory_to_scan = 'C:/Users/HP/Downloads'

if os.path.exists(directory_to_scan):
    organize_files(directory_to_scan)
else:
    print(f"Error: The directory '{directory_to_scan}' does not exist.")

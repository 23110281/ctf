unziped the file using `unzip` and found it was recursively creating new files so
opened up the zip file in a text editor and searched for flag and found that it was there after a while (~12000) lines so i wrote to script to unzip the files inf which i quickly realised would make the storage burst as it was 1.8 mb each file so i updated the script to delete the file and then added a 0.1 sec wait so my cpu doesn't overheat and waited approx 20 mins (12000x0.1) for it to reach the flag and then stopped it when it reached the flag.txt (which i found from file.txtUT and rando.zipUT), i used cgpt to create the script

here's the script
`#!/bin/bash
while true; do
    if [ -e "flag.txt" ]; then
        echo "Found 'flag.zip'. Stopping the script."
        exit 0
    fi
    # Query the current directory for zip files
    zip_file=$(find . -maxdepth 1 -type f -name "*.zip" | head -n 1)
    # Check if a zip file was found
    if [ -n "$zip_file" ]; then
        echo "Processing $zip_file..."
        # Unzip the zip file
        unzip -q "$zip_file"
        # Delete the first zip file and keep the others
        # find . -maxdepth 1 -type f -name "*.zip" -not -name "$zip_file" -exec rm {} \;
        rm $zip_file
        echo "Deleted $zip_file."
    else
        echo "No zip files found in the directory!"
        exit 1
    fi
    # Sleep for a while (0.5 seconds in this case)
    sleep 0.1
done
`
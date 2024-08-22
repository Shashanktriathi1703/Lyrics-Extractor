# Lyrics-Extractor

Lyrics-Extractor is an innovative Python application that boasts a user-friendly interface designed with Tkinter, enabling seamless interaction for users. It also incorporates MySQL database connectivity, allowing for efficient data management and retrieval. Additionally, the application utilizes the Genius API to access a comprehensive range of music data, enhancing the overall user experience. To ensure security and user privacy, individuals can sign up for the application and log in by using one-time password (OTP) authentication. This feature facilitates a secure access point to a wealth of music-related information, making it a valuable tool for music lovers and enthusiasts alike.

## Features

- User Authentication: New users can easily sign up for an account, and existing users can log in to access the application's features.
- Lyrics Extraction: The application integrates with the Genius API to extract music-related information such as lyrics, artist details, and song details.
- Database Connectivity: MySQL is used to store user information and authentication details securely.

## Requirements

- Python 3.11
- Tkinter
- MySQL Server
- Genius API access token

## Installation and Setup

1. Clone the Lyrics-Extractor repository from GitHub.
2. Install the required dependencies using `pip install -r requirements.txt`.
3. Set up a MySQL database for the application and update the database connection details in the configuration files.
4. Obtain a Genius API access token and update the application with the token for music extraction.

## Configuration

The application requires the following configurations:

### MySQL Database Configuration

- Host: [Your MySQL Host]
- Database Name: [Your Database Name]
- Username: [Your Username]
- Password: [Your Password]

### Genius API Configuration

- Access Token: Obtain a Genius API key from `https://genius.com/api-clients`.

## Data Flow
![flow](https://github.com/user-attachments/assets/db94896c-3c8b-43f1-93ce-7bd3e22f03f3)



## Usage

1. Run the application using `python lyrics.py`.
2. Sign up for a new account or log in with existing credentials.
3. Use the music extraction feature to search for and retrieve music-related information using the `Genius API`.

## Demo

- Signup

![Screenshot 2023-10-08 121419](https://github.com/Shashanktriathi1703/Music-Extractor/assets/105815482/857844e6-5e73-4e68-a75e-731fb73ab2f9)

- OTP

![otp](https://github.com/user-attachments/assets/d8e1f002-9568-4f90-9e1c-71abb1faf198)

- Login
  
![Screenshot 2023-10-08 121518](https://github.com/Shashanktriathi1703/Music-Extractor/assets/105815482/a0b8327b-19c1-4907-81b6-49f58c56cb97)

- Music-Extractor
  
![Screenshot 2023-10-09 000654](https://github.com/Shashanktriathi1703/Music-Extractor/assets/105815482/bee25bec-ee9a-4a38-97b2-9966ea8be7b2)

## Contributors

- `SHASHANK TRIPATHI`

## License

This project is licensed under the `LI-MAT SOLUTION` License - see the LICENSE file for details.

## Acknowledgements

- The Music-Extractor application uses Tkinter for the user interface, MySQL for database connectivity, and the Genius API for music extraction. We acknowledge and thank the developers and communities behind these technologies for their valuable contributions.


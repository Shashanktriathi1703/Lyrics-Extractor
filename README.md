# Music-Extractor

Music-Extractor is a Python application that utilizes Python Tkinter for the user interface, MySQL for database connectivity, and the Genius API for music extraction. This application allows users to sign up, log in, and access music-related information using the Genius API.

## Features

- User Authentication: New users can easily sign up for an account, and existing users can log in to access the application's features.
- Music Extraction: The application integrates with the Genius API to extract music-related information such as lyrics, artist details, and song details.
- Database Connectivity: MySQL is used to store user information and authentication details securely.

## Requirements

- Python 3.11
- Tkinter
- MySQL Server
- Genius API access token

## Installation and Setup

1. Clone the Music-Extractor repository from GitHub.
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

## Usage

1. Run the application using `python lyrics.py`.
2. Sign up for a new account or log in with existing credentials.
3. Use the music extraction feature to search for and retrieve music-related information using the `Genius API`.

## Contributors

- `SHASHANK TRIPATHI`

## License

This project is licensed under the `LI-MAT SOLUTION` License - see the LICENSE file for details.

## Acknowledgements

- The Music-Extractor application uses Tkinter for the user interface, MySQL for database connectivity, and the Genius API for music extraction. We acknowledge and thank the developers and communities behind these technologies for their valuable contributions.


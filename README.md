# Gallery-Hacks
from cryptography.fernet import Fernet
from PIL import Image
import io

# Generate a key for encryption
key = Fernet.generate_key()
cipher = Fernet(key)

# Function to encrypt an image
def encrypt_image(image_path, output_path):
    with open(image_path, "rb") as image_file:
        image_data = image_file.read()
    
    encrypted_data = cipher.encrypt(image_data)
    
    with open(output_path, "wb") as encrypted_file:
        encrypted_file.write(encrypted_data)

# Function to decrypt an image
def decrypt_image(encrypted_path, output_path):
    with open(encrypted_path, "rb") as encrypted_file:
        encrypted_data = encrypted_file.read()
    
    decrypted_data = cipher.decrypt(encrypted_data)
    
    with open(output_path, "wb") as decrypted_file:
        decrypted_file.write(decrypted_data)

# Example usage
encrypt_image("example.jpg", "encrypted_image.enc")
decrypt_image("encrypted_image.enc", "decrypted_image.jpg")

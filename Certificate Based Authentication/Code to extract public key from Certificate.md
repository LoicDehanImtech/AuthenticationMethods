from cryptography import x509
from cryptography.hazmat.primitives import serialization
// Use default_backend() if required by your cryptography version, often implicit now
//from cryptography.hazmat.backends import default_backend

//--- Configuration ---
//Provide the path to the certificate file (usually .pem, .crt, .cer)
certificate_file_path = 'path/to/your/certificate.pem'

//NOTE: You DO NOT need the private key file path for this operation.
//The public key is *inside* the certificate file.

try:
    # --- Load the certificate file ---
    # Read the certificate file in binary mode
    with open(certificate_file_path, "rb") as cert_file:
        cert_data = cert_file.read()

    # --- Parse the certificate ---
    # This assumes the certificate is in PEM format (common text format)
    # If it's in DER format (binary), use x509.load_der_x509_certificate(cert_data)
    try:
        certificate = x509.load_pem_x509_certificate(cert_data)
        print(f"Successfully loaded PEM certificate from: {certificate_file_path}")
    except ValueError as pem_error:
        # Try loading as DER if PEM fails
        try:
            certificate = x509.load_der_x509_certificate(cert_data)
            print(f"Successfully loaded DER certificate from: {certificate_file_path}")
        except ValueError as der_error:
            print(f"Error: Could not parse certificate file as PEM or DER.")
            print(f"PEM Error: {pem_error}")
            print(f"DER Error: {der_error}")
            exit() # Exit if parsing fails

    # --- Extract the public key object ---
    public_key_obj = certificate.public_key()

    # --- Serialize the public key object to a standard format (PEM) for display ---
    public_key_pem = public_key_obj.public_bytes(
        encoding=serialization.Encoding.PEM,
        # SubjectPublicKeyInfo is a standard format for public keys
        format=serialization.PublicFormat.SubjectPublicKeyInfo
    )

    # --- Print the public key ---
    print("\n--- Extracted Public Key (PEM Format) ---")
    print(public_key_pem.decode('utf-8')) # Decode bytes to string for printing

    # You can also get details about the key type and size
    key_type = type(public_key_obj).__name__
    key_size = getattr(public_key_obj, 'key_size', 'N/A') # key_size attribute exists for RSA, EC, etc.
    print(f"\nKey Type: {key_type}")
    print(f"Key Size: {key_size} bits")


except FileNotFoundError:
    print(f"Error: Certificate file not found at '{certificate_file_path}'")
except Exception as e:
    # Catch any other unexpected errors during file handling or processing
    print(f"An unexpected error occurred: {e}")
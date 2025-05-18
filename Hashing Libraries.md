

## 1. BCrypt.Net-Next
1. Algoritme, geen echte keuze, maar compatibel met alles. Enkel .net runtime nodig
- Work factor (4-31): Higher = more secure but slower (recommended: 10-12)
$2a$12\$R9h/cIPz0gi.URNNX3kh2OPST9/PgBkqquzi.Ss7KIUgO2t0jWMUW
│  │  │                       │
│  │  │                       └─ Hash (31 chars)
│  │  └─ Salt (22 chars)
│  └─ Cost factor (12)
└─ Algorithm version ($2a)

string hash = BCrypt.Net.BCrypt.HashPassword(password, 12);
bool isValid = BCrypt.Net.BCrypt.Verify(password, hash);

PasswordHash VARCHAR(60) -- BCrypt hashes are always 60 characters );

Eventueel meermaals hashen?

 var doubleBcryptSaltGiven = BCrypt.HashPassword(BCrypt.HashPassword(pass, salt), salt);
            var doubleBcryptFullHashGivenAsSalt = BCrypt.HashPassword(BCrypt.HashPassword(pass, passwordHashTwoRound), passwordHashTwoRound);


Optie voor pre-hashing met SHA naar keuze:
- string hashed = BCryptExtendedV2.HashPassword(plain, salt, HashType.SHA256);
  ## 1. **Password Length Limitations**
	**Problem**: BCrypt has a practical input limit of around 72 bytes. Longer passwords get truncated.
	## 2. **Unicode and Character Set Issues**

	**Problem**: BCrypt was designed for ASCII/UTF-8, and some implementations have issues with certain Unicode characters.
	- **Null Bytes**: Terminates at first null byte (`\0`)
	- **Encoding**: Input is treated as UTF-8 byte array
## 2. Argon2 Libraries (Most secure modern option) (Konscious.Security.Cryptography)
- **Compatibility**: .NET Framework 4.6.1+, .NET Core 2.0+, .NET 5+
-
var argon2 = new Argon2id(Encoding.UTF8.GetBytes("password")); 
argon2.Salt = GenerateSalt(); // 16+ bytes recommended 
argon2.DegreeOfParallelism = 8; 
argon2.Iterations = 4; 
argon2.MemorySize = 1024 * 1024; // 1 GB 
byte[] hash = argon2.GetBytes(16);

**Configurable parameters**:

- Memory cost (KB): Amount of memory used
- Time cost (iterations): Number of iterations
- Parallelism: Number of threads
- Hash length: Output size in bytes
- Variant: Argon2d (GPU-resistant), Argon2i (side-channel resistant), Argon2id (hybrid)

## 2.B Isopoh.Cryptography.Argon2

	Alternative Argon2 implementation
	
	- Compatibility**: .NET Framework 4.5+, .NET Standard 2.0+
	- Same Argon2 algorithm with similar configuration options
## 3. Built-in .NET Options: Rfc2898DeriveBytes (PBKDF2)
**Compatibility**: .NET Framework 2.0+, .NET Core, .NET 5+
Hash algorithms: SHA1, SHA256, SHA384, SHA512
- Iteration count: 10,000+ recommended (100,000+ for high security)
 - **Use SHA256**(32 bytes) for most applications (good balance of security and performance)
- **Use SHA384(48 bytes)/SHA512(64 bytes)** when maximum security is required or mandated by regulations
using (var rfc2898 = new Rfc2898DeriveBytes("password", salt, 10000)) 
{ byte[] hash = rfc2898.GetBytes(20); }



Memory Usage:
- **PBKDF2**: ~4KB (minimal)
- **BCrypt**: Its fixed memory usage (4KB) is a limitation compared to more modern algorithms. 
- **Argon2**: We can see with a time cost of 8 and a memory cost of 128MB, it will take 1,467 ms.
Strength
- PBKDF2: Fastest of the four, but this is a drawback for password hashing. Low memory usage makes it vulnerable to parallel attacks. 
- bcrypt: Generally slower than PBKDF2 but faster than scrypt. [Security Boulevard](https://securityboulevard.com/2024/07/comparative-analysis-of-password-hashing-algorithms-argon2-bcrypt-scrypt-and-pbkdf2/)[Deepak Gupta](https://guptadeepak.com/comparative-analysis-of-password-hashing-algorithms-argon2-bcrypt-scrypt-and-pbkdf2/)
- scrypt: Moderate speed, High memory usage, which can be a limitation in resource-constrained environments. Slower than bcrypt and PBKDF2.
- Argon2: Most configurable but generally slowest




| Algorithm              | CPU (single core) | GPU (high-end) | ASIC/FPGA    | Memory Usage |
| ---------------------- | ----------------- | -------------- | ------------ | ------------ |
| **SHA-256 only**       | 10 million        | 10 billion     | 100+ billion | ~4KB         |
| **PBKDF2 (100K iter)** | 1,000             | 100,000        | 1+ million   | ~4KB         |
| **BCrypt (factor 12)** | 1,000             | 10,000         | 50,000       | 4KB fixed    |
| **Argon2id (128MB)**   | 100               | 1,000          | 5,000        | 128MB - 1GB+ |
| **scrypt (16MB)**      | 500               | 5,000          | 25,000       | 16MB-1GB     |


| Library                 | Max Password Length | Character Support | Null Byte Handling | Encoding            |
| ----------------------- | ------------------- | ----------------- | ------------------ | ------------------- |
| **Built-in PBKDF2**     | Unlimited           | Full Unicode      | ✅ Preserved        | UTF-8/UTF-16/Custom |
| **BCrypt.Net-Next**     | ~72 bytes*          | UTF-8 Unicode     | ❌ Truncates        | UTF-8               |
| **BCrypt Extended V2**  | Unlimited           | Full Unicode      | ✅ Preserved        | UTF-8 (pre-hashed)  |
| **AspNetCore.Identity** | Unlimited           | Full Unicode      | ✅ Preserved        | UTF-8               |
| **Argon2 (Konscious)**  | Unlimited           | Full Unicode      | ✅ Preserved        | UTF-8/Byte array    |
| **scrypt.NET**          | Unlimited           | Full Unicode      | ✅ Preserved        | UTF-8/Byte array    |


| Library                 | x86 (32-bit)   | x64 (64-bit) | ARM32          | ARM64  | Memory Requirements |
| ----------------------- | -------------- | ------------ | -------------- | ------ | ------------------- |
| **Built-in PBKDF2**     | ✅ Full         | ✅ Full       | ✅ Full         | ✅ Full | ~4KB                |
| **BCrypt.Net-Next**     | ✅ Full         | ✅ Full       | ✅ Full         | ✅ Full | ~4KB                |
| **AspNetCore.Identity** | ✅ Full         | ✅ Full       | ✅ Full         | ✅ Full | ~4KB + Framework    |
| **Argon2 (Konscious)**  | ⚠️ Limited RAM | ✅ Full       | ⚠️ Limited RAM | ✅ Full | 64MB-1GB+           |
| **scrypt.NET**          | ⚠️ Limited RAM | ✅ Full       | ⚠️ Limited RAM | ✅ Full | 16MB-1GB            |
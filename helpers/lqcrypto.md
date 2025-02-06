# LQCrypto Helper

Secure cryptographic operations helper for Go applications.


## Usage

```go
import "github.com/go-liquor/liquor-sdk/helpers/lqcrypto"
```

## Features

- Password hashing using bcrypt
- AES-GCM encryption/decryption
- Secure key generation
- Hash comparison

## Configuration

In your configuration file:
```yaml
password:
    bcrypt_cost: 12  # Default bcrypt cost (recommended: 10-14)
```

## Examples

### Initialize the Helper

```go
crypto := lqcrypto.NewCryptoHelper(config)
```

### Password Hashing

```go
// Hash a password
password := "mySecurePassword123"
hashedPassword, err := crypto.Hash(password)
if err != nil {
    // Handle error
}

// Verify password
isValid := crypto.CompareHash(hashedPassword, password) // returns true
isInvalid := crypto.CompareHash(hashedPassword, "wrongPassword") // returns false
```

### Data Encryption/Decryption

```go
// Generate a secure key
key, err := crypto.GenerateKey(256) // 256-bit key
if err != nil {
    // Handle error
}

// Encrypt data
data := []byte("sensitive information")
encrypted, err := crypto.Encrypt(data, key)
if err != nil {
    // Handle error
}

// Decrypt data
decrypted, err := crypto.Decrypt(encrypted, key)
if err != nil {
    // Handle error
}
```

## Security Considerations

### Password Hashing
- The bcrypt cost parameter affects the hashing time and security level
- Higher cost values provide better security but require more processing time
- Recommended cost values: 10-14 (depending on your server's performance)

### Encryption
- AES-GCM provides both confidentiality and authenticity
- Supported key sizes:
  - 128 bits (16 bytes)
  - 192 bits (24 bytes)
  - 256 bits (32 bytes)
- Always use secure key storage
- Never reuse nonces (handled automatically by the implementation)

## Best Practices

1. Key Management
```go
// Generate a secure key
key, err := crypto.GenerateKey(256)
if err != nil {
    // Handle error
}

// Store the key securely
// Never store encryption keys in plain text
```

2. Password Hashing
```go
// Hash password before storage
hashedPassword, err := crypto.Hash(userPassword)
if err != nil {
    // Handle error
}

// Store hashedPassword in database
```

3. Secure Data Encryption
```go
// Encrypt sensitive data
encrypted, err := crypto.Encrypt(sensitiveData, key)
if err != nil {
    // Handle error
}

// Store encrypted data
// Keep encryption key separate from encrypted data
```

## Error Handling

The package provides detailed error handling for various scenarios:

```go
// Handle hashing errors
hashedPassword, err := crypto.Hash(password)
if err != nil {
    switch err {
    case bcrypt.ErrHashTooShort:
        // Handle invalid hash
    default:
        // Handle other errors
    }
}

// Handle decryption errors
decrypted, err := crypto.Decrypt(encrypted, key)
if err != nil {
    switch {
    case errors.Is(err, errors.New("encrypted data too short")):
        // Handle invalid encrypted data
    default:
        // Handle other errors
    }
}
```

## Thread Safety

The CryptoHelper is safe for concurrent use by multiple goroutines.

## Dependencies

- golang.org/x/crypto/bcrypt
- crypto/aes
- crypto/cipher
- crypto/rand


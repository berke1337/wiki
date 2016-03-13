# Encryption
Sometimes you simply want to encrypt a file, e.g. the database backup file.

Encrypt: `openssl aes-256-cbc -salt -in file.tar -out file.tar.enc`
Decrypt: `openssl aes-256-cbc -d -in file.tar.enc -out file.tar.new`

You can also pipe to it by not specifying the `-in` parameter. 

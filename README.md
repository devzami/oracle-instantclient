# Oracle Instant Client Installation for Linux x86-64 (64-bit)

## 📘 General Information
- For general Instant Client details, visit the [Home Page](https://www.oracle.com/database/technologies/instant-client.html).
- ODBC users should refer to the [ODBC Installation Instructions](https://www.oracle.com/database/technologies/instant-client-odbc-downloads.html).
- See the [Database Client Installation Guide for Linux](https://docs.oracle.com/en/database/) for detailed instructions.
- RPMs are available on [yum.oracle.com](https://yum.oracle.com) for Oracle Linux versions.
- Client-server version interoperability is explained in [Doc ID 207303.1](https://support.oracle.com/epmos/faces/DocumentDisplay?id=207303.1).

## ⚙️ Installation Using ZIP Files

### 1. 📥 Download and Extract
- Download the desired ZIP files (Basic or Basic Light is required).
- Unzip into a directory (e.g., `/opt/oracle/instantclient_12_2`).

```bash
cd /opt/oracle      
unzip instantclient-basic-linux.x64--12.2.0.1.0.zip
```

### 2. 🔗 Create Symbolic Links (For versions < 18.3)

```bash
cd /opt/oracle/instantclient_12_2
ln -s libclntsh.so.12.1 libclntsh.so
ln -s libocci.so.12.1 libocci.so
```

### 3. 🛠 Install Required Libraries

```bash
sudo yum install libaio
```

For Oracle Linux 8 (prior to Instant Client 21):

```bash
sudo yum install libnsl
```

### 4. 📂 Configure Runtime Link Path
If Instant Client is the only Oracle software installed:

```bash
sudo sh -c "echo /opt/oracle/instantclient_19_3 > /etc/ld.so.conf.d/oracle-instantclient.conf"
sudo ldconfig
```

Alternatively, set the `LD_LIBRARY_PATH` environment variable:

```bash
export LD_LIBRARY_PATH=/opt/oracle/instantclient_19_3:$LD_LIBRARY_PATH
```

(Optional: Add this to `~/.bash_profile` or `/etc/sysconfig/httpd`.)

### 5. 📜 Oracle Configuration Files
To co-locate configuration files (e.g., `tnsnames.ora`, `sqlnet.ora`):

```bash
mkdir -p /opt/oracle/instantclient_12_2/network/admin
```

Alternatively, set the `TNS_ADMIN` environment variable to the configuration directory:

```bash
export TNS_ADMIN=/path/to/config/directory
```

### 6. 🔗 Update PATH for SQL*Plus
If using `sqlplus`, unzip the package in the same directory as the Basic package and update `PATH`:

```bash
export PATH=/opt/oracle/instantclient_19_3:$PATH
```

### 7. 🚀 Start Your Application

## 📦 Installation Using RPM Files

### 1. 📥 Download and Install RPM Packages

```bash
sudo yum install oracle-instantclient19.3-basic-19.3.0.0.0-1.x86_64.rpm
```

### 2. 📂 Configure Runtime Link Path (For versions < 19.3)

```bash
sudo sh -c "echo /usr/lib/oracle/18.3/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf"
sudo ldconfig
```

For versions 19.3 and later, this step is automated.

### 3. 🔗 Environment Variable Alternative
Set `LD_LIBRARY_PATH` manually:

```bash
export LD_LIBRARY_PATH=/usr/lib/oracle/18.3/client64/lib:$LD_LIBRARY_PATH
```

(Optional: Add this to `~/.bash_profile` or `/etc/sysconfig/httpd`.)

### 4. 📜 Oracle Configuration Files
Create the default configuration directory:

```bash
sudo mkdir -p /usr/lib/oracle/12.2/client64/lib/network/admin
```

Alternatively, set `TNS_ADMIN`:

```bash
export TNS_ADMIN=/path/to/config/directory
```

### 5. 🔗 Update PATH for Tools

```bash
export PATH=/usr/lib/oracle/19.3/client64/bin:$PATH
```

### 6. 🚀 Start Your Application

---

### 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### 🔑 Support

For any issues or support requests, feel free to open an issue in this repository.

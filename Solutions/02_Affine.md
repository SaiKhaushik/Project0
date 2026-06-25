# **Affine Cipher**

# **Objective**

The second solution considered was implementing an **Affine Cipher** by using the UAV's **latitude** and **longitude** as dynamic encryption keys. The goal was to make the encryption dependent on the UAV's current geographical location instead of using fixed keys.

# **Why We Considered Affine Cipher**

After rejecting **Two-Factor Authentication (2FA)**, we explored lightweight encryption techniques that could provide basic confidentiality for MAVLink messages.

We selected the **Affine Cipher** because:

- It is simple to implement.
- It has low computational overhead.
- It allows the use of mathematical keys for encryption.
- Latitude and longitude values are continuously updated during flight, making them suitable as dynamic inputs for key generation.

Our idea was to use:

- **Latitude** as the multiplicative key (**a**)
- **Longitude** as the additive key (**b**)

Since the UAV continuously changes its position, the encryption keys would also change dynamically throughout the flight.

# **Our Approach**

The Affine Cipher follows the equation:

> **E(x) = (ax + b) mod m**

where:

- **a** = Latitude-derived key
- **b** = Longitude-derived key

The latitude and longitude values obtained from the UAV's GPS were converted into valid integer keys before encryption.

Every MAVLink message was encrypted using these dynamically generated keys before transmission.

# **Result**

The implementation successfully demonstrated **location-dependent encryption**, where encrypted messages changed as the UAV moved to different locations.

However, despite introducing dynamic keys, the Affine Cipher remained a **classical encryption algorithm** with limited security.

# **Limitations**

- Provides only **basic confidentiality**.
- Does **not provide message integrity**.
- Does **not authenticate the sender**.
- Vulnerable to **known-plaintext** and **frequency analysis** attacks.
- Does **not prevent replay attacks**.
- Does **not prevent Man-in-the-Middle (MITM) attacks**.
- The security of the cipher is insufficient for protecting modern UAV communication.

# **Conclusion**

Although using **latitude** and **longitude** as dynamic keys introduced a novel location-aware encryption concept, the **Affine Cipher itself was not cryptographically strong enough** to secure MAVLink communication.

Since it could not provide **confidentiality, integrity, and authentication** at the required security level, we rejected it as the final solution and continued exploring stronger cryptographic algorithms.

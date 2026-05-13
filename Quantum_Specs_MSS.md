# Technical Specifications: Stateless Post-Quantum MSS Architecture

1. Cryptographic Primitive

Algorithm: Double-SHA256 (SHA256d / Bitcoin Standard).

Security Strength: 128-bit Post-Quantum resistance (mitigating Grover’s Algorithm).

Output: 256-bit (32-byte) uint256 digest for full protocol compatibility.

2. Tree Topology & Balancing

Structure: Binary Merkle Tree.

Balancing Logic: Tail-End Duplication. If \(N\) is odd, duplicate the final leaf. This prevents the "dangling hash" vulnerability (CVE-2012-2459) and ensures cryptographic integrity across all levels.

Capacity: Supports up to \(2^{32}\) leaves (OTS keys) per Merkle Root.

3. Performance & Memory Optimization

Complexity: \(O(N)\) for leaf processing; \(O(\log N)\) for audit path verification.

Memory Management: Utilizes std::move and std::vector::reserve to eliminate heap fragmentation and minimize CPU cycle waste during high-frequency validation.

Verification: Stateless verification using Audit Paths to keep transaction (PSBT) sizes "Punctual" and small.

4. Integration Architecture

BIP-322 Link: Designed as the future-proof security layer for the now-merged "Proof of Funds" logic.

Target: Integration into src/crypto/ for Bitcoin Core, providing a Reference Implementation for Merkle-based Post-Quantum Signatures.

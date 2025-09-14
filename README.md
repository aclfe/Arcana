# Neural Cryptography via Adversarial Networks

## Automated Cryptographic Design using GANs

The system uses adversarial training to automatically discover encryption schemes without explicit cryptographic programming.

## Core Architecture

### Networks
- **Alice (Encryptor)**: Learns to transform plaintext into secure ciphertext using a shared key
- **Bob (Decryptor)**: Learns to decrypt Alice's ciphertext back to plaintext using the same shared key  
- **Eve (Adversary)**: Two adversarial networks that try to:
  - **Discriminator**: Detect if ciphertext is real or random noise
  - **Decoder**: Reconstruct the original message without access to the key

### Training Process
1. **Cooperative Phase**: Alice and Bob train together to maximize communication accuracy
2. **Adversarial Phase**: Eve trains to break Alice's encryption while Alice learns to fool Eve
3. **Convergence**: System reaches equilibrium where Bob can decrypt perfectly but Eve performs no better than random guessing

## Getting Started

### Prerequisites
```bash
# Install dependencies
pip install -r requirements.txt

# For GPU training (optional but recommended)
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
```

### Usage
1. **Open Jupyter Notebook**:
   ```bash
   jupyter notebook showcase_raw_Arcana.ipynb
   ```

2. **Run All Cells**: Execute each cell sequentially to:
   - Set up networks and configuration
   - Train the adversarial system
   - Visualize results and analyze performance

3. **Monitor Training**: Watch for these success metrics:
   - Bob Accuracy → 1.0 (perfect decryption)
   - Eve Discriminator Accuracy → 0.5 (random guessing)
   - Eve Decoder Accuracy → 0.5 (random guessing)

## Configuration

Key parameters in the `Config` class:
- `MESSAGE_LENGTH`: Length of plaintext/ciphertext (default: 16 bits)
- `KEY_LENGTH`: Length of shared key (default: 16 bits)
- `BATCH_SIZE`: Training batch size (default: 512)
- `NUM_EPOCHS`: Total training epochs (default: 1000)
- `HIDDEN_SIZE`: Network hidden layer size (default: 64)

## Expected Results

A successful training should show:
- **Alice Loss**: Decreases over time as she learns to fool Eve while helping Bob
- **Bob Accuracy**: Quickly approaches 100% and stays high
- **Eve Discriminator**: Starts high but drops to ~50% (random guessing)
- **Eve Decoder**: Fluctuates around ~50% (unable to decode messages)

## Experiments to Try

1. **Scale Testing**: Increase message/key lengths to test scalability
2. **Architecture Variations**: Try CNNs, RNNs, or Transformer architectures
3. **Multiple Adversaries**: Add more Eve networks with different strategies
4. **Noise Channels**: Simulate real-world communication with noise
5. **Key Management**: Experiment with dynamic or one-time keys

## Technical Details

### Loss Functions
- **Reconstruction Loss**: Binary cross-entropy for Alice-Bob communication
- **Adversarial Loss**: GAN-style loss for Alice vs Eve competition
- **Combined Loss**: Weighted combination encouraging cooperation and adversarial behavior

### Network Architecture
- **Fully Connected**: Dense layers with ReLU activations and dropout
- **Input/Output**: Sigmoid activation for binary data representation
- **Scalable**: Configurable depth and width for different problem sizes


## Performance Tips

### For Better Results:
- Use GPU acceleration (CUDA) when available
- Experiment with learning rates and training ratios
- Try different network architectures for larger message sizes
- Monitor training curves to detect convergence issues

### Troubleshooting:
- If Bob accuracy doesn't improve: Reduce learning rates or increase reconstruction weight
- If Eve performs too well: Increase adversarial weight or train Eve less frequently
- For unstable training: Add more dropout or reduce learning rates

## What This Demonstrates

1. **Emergent Security**: Cryptographic security emerges from adversarial training without explicit programming
2. **Measurable Security**: Eve's random performance quantifies encryption strength  
3. **Automated Design**: Machine learning can discover novel cryptographic schemes
4. **Practical Applications**: Foundation for adaptive, learnable security systems

---

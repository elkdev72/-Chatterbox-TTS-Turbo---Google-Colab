# 🎙️ Chatterbox TTS Turbo - Google Colab

Run [Chatterbox TTS Turbo](https://github.com/devnen/chatterbox-v2) on Google Colab with GPU acceleration for high-quality text-to-speech synthesis.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/elkdev72/-Chatterbox-TTS-Turbo---Google-Colab/blob/main/Chatterbox_TTS_Turbo_Documented.ipynb)

## ✨ Features

- 🚀 **One-Click Setup** - Run the entire setup with just a few clicks
- ⚡ **GPU Accelerated** - Leverages Google Colab's free GPU for fast generation
- 🎨 **28+ Predefined Voices** - Choose from a variety of high-quality voices
- 🎭 **Voice Cloning** - Upload your own audio to create custom voices
- 😄 **Paralinguistic Tags** - Add emotions with `[laugh]`, `[sigh]`, `[gasp]`, and more
- 🌐 **Web Interface** - User-friendly UI for easy text-to-speech generation
- 📡 **REST API** - Programmatic access for integration

## 🎯 Quick Start

1. **Open the Notebook**
   - Click the "Open in Colab" badge above
   - Or [click here](https://colab.research.google.com/github/elkdev72/-Chatterbox-TTS-Turbo---Google-Colab/blob/main/Chatterbox_TTS_Turbo_Documented.ipynb)

2. **Enable GPU Runtime**
   - Go to `Runtime` → `Change runtime type`
   - Select `T4 GPU` (or better) from the Hardware accelerator dropdown
   - Click `Save`

3. **Run All Cells**
   - Click `Runtime` → `Run all`
   - Wait ~3-5 minutes for setup to complete
   - Click the link that appears to open the Web UI

4. **Generate Speech!**
   - Select a voice or upload your own
   - Enter your text
   - Click "Generate" and download your audio

## 📋 Requirements

- Google account (for Colab access)
- GPU runtime (free tier works great)
- ~5GB storage for models and dependencies
- 3-5 minutes for initial setup

## 🛠️ What Gets Installed

The notebook automatically sets up:

- **Python 3.11** environment (isolated via micromamba)
- **PyTorch 2.5.1** with CUDA 12.1 support
- **Chatterbox TTS Turbo** package (latest from GitHub)
- **TTS Server** with FastAPI web interface
- **Compatibility patches** for recent package changes

## 🎨 Available Voices

The notebook includes 28+ predefined voices:

- **Female**: Emily, Jessica, Sarah, Madison, Michelle, Ashley, Nicole, Samantha, Emma, Laura
- **Male**: Jacob, Michael, Matthew, Joshua, Andrew, Daniel, Christopher, James, Ryan, David
- **And more!**

You can also upload your own audio file (10-30 seconds) to clone any voice.

## 💡 Usage Examples

### Basic Text-to-Speech

```
Hello! Welcome to Chatterbox TTS. This is a simple example.
```

### With Paralinguistic Tags

```
Oh wow! [gasp] I can't believe this works so well. [laugh]
That's actually amazing. [sigh] Technology these days, right?
```

### Supported Tags

- `[laugh]` - Laughter
- `[chuckle]` - Light laughter
- `[sigh]` - Sighing
- `[gasp]` - Surprise/shock
- `[cough]` - Coughing
- `[clear throat]` - Throat clearing
- `[sniff]` - Sniffing
- `[groan]` - Groaning
- `[shush]` - Shushing sound

## 🔧 Advanced Configuration

### Adjustable Parameters

- **Temperature** (0.7-0.9): Controls randomness and expressiveness
- **Repetition Penalty** (1.0-1.5): Reduces repeated phrases
- **Seed**: Use the same seed for reproducible results
- **Top-p Sampling**: Controls diversity of generation
- **Top-k Sampling**: Limits vocabulary at each step

### API Usage

The server exposes a REST API at `/tts`:

```bash
curl -X POST "http://localhost:8004/tts" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Hello world!",
    "voice": "Emily.wav",
    "temperature": 0.8,
    "seed": 42
  }' \
  --output output.wav
```

See full API docs at `http://localhost:8004/docs` when the server is running.

## 📊 Performance

| Task | First Run | Subsequent Runs |
|------|-----------|-----------------|
| Environment Setup | ~3-5 min | N/A |
| Model Download | ~2-3 min | Cached |
| First Generation | ~30-60 sec | ~5-15 sec |
| Per Generation | ~5-15 sec | ~5-15 sec |

*Times vary based on text length and Colab's available resources*

## 🐛 Troubleshooting

### CUDA Out of Memory

```
Runtime → Factory reset runtime
```

Then re-run all cells.

### Model Fails to Load

Make sure Cell 4 (compatibility patch) ran successfully. Look for:
```
✅ Patched watermarker initialization
✅ Patched watermark application in generate()
```

### Server Won't Start

1. Verify you're using a GPU runtime (not CPU)
2. Check all previous cells completed successfully
3. Look for error messages in the cell output

### Slow Generation

- First generation is always slower (model warmup)
- Subsequent generations use cached models and are faster
- Longer text is automatically chunked and may take more time

### Connection Issues

If the Web UI link doesn't work:
- Try the alternative: `Runtime → Manage sessions → Click the port 8004 link`
- Or use the API endpoint directly: `http://localhost:8004`

## 🔒 Privacy & Data

- All processing happens on Google Colab's servers
- No data is sent to external services (except model downloads from HuggingFace)
- Custom voice files are stored temporarily in the Colab session
- Everything is deleted when the runtime is closed

## 📁 File Structure

```
/content/
├── bin/
│   └── micromamba           # Environment manager
├── hf_home/                 # HuggingFace cache (models)
├── Chatterbox-TTS-Server/   # Server code
│   ├── voices/              # Predefined voice files
│   ├── server.py            # Main server
│   └── config.yaml          # Configuration
└── chatterbox_server_stdout.log  # Server logs
```

## 🤝 Contributing

Found a bug or have a suggestion?

1. Check existing issues in this repository
2. For Chatterbox TTS issues, report to [devnen/chatterbox-v2](https://github.com/devnen/chatterbox-v2/issues)
3. For server issues, report to [devnen/Chatterbox-TTS-Server](https://github.com/devnen/Chatterbox-TTS-Server/issues)

## 📜 License

This notebook and repository: MIT License

Chatterbox TTS: See [original repository](https://github.com/devnen/chatterbox-v2) for license details

## 🙏 Credits

- **Chatterbox TTS** by [devnen](https://github.com/devnen)
- **Chatterbox TTS Server** by [devnen](https://github.com/devnen)
- This Colab notebook is a community contribution for easier access

## 🔗 Links

- [Chatterbox TTS GitHub](https://github.com/devnen/chatterbox-v2)
- [Chatterbox Server GitHub](https://github.com/devnen/Chatterbox-TTS-Server)
- [HuggingFace Model](https://huggingface.co/Pendrokar/chatterbox-tts)
- [Original Paper/Demo](https://example.com) *(if available)*

## ⚠️ Notes

- Google Colab sessions are temporary and will disconnect after ~12 hours of inactivity
- Models are re-downloaded each time you restart the runtime (not persistent)
- For production use, consider deploying to a persistent server
- GPU availability on Colab free tier may vary based on demand

## 📝 Changelog

### v1.0.0 (February 2026)
- Initial release
- Full documentation
- Compatibility patches for watermarker issues
- 28+ predefined voices
- Web UI and REST API

## 💬 Support

Need help? Here's where to ask:

- **This notebook**: Open an issue in this repository
- **Chatterbox TTS**: [GitHub Issues](https://github.com/devnen/chatterbox-v2/issues)
- **Server**: [GitHub Issues](https://github.com/devnen/Chatterbox-TTS-Server/issues)

---

**Made with ❤️ for the TTS community**

If this helped you, consider:
- ⭐ Starring this repository
- ⭐ Starring [Chatterbox TTS](https://github.com/devnen/chatterbox-v2)
- 📢 Sharing with others who might find it useful

## 1. Introduction

[← Back to Table of Contents](00-TOC.md)

### 1.1 About Tvheadend

Tvheadend is a powerful, open-source TV streaming server and Digital Video Recorder (DVR) for Linux, supporting a wide range of input sources and output protocols. It acts as a central hub for receiving, processing, and distributing live television and radio streams throughout your network, while also providing comprehensive recording and time-shifting capabilities.

**Key Capabilities:**

**Input Sources:**
- **DVB (Digital Video Broadcasting)**: Native support for DVB-S/S2 (satellite), DVB-T/T2 (terrestrial), DVB-C/C2 (cable), and ATSC (North American digital TV) via Linux DVB API
- **IPTV**: HTTP, UDP, and pipe-based IPTV streams with support for M3U playlists
- **SAT>IP**: Network-based satellite receivers using the SAT>IP protocol
- **HDHomeRun**: Network tuners from SiliconDust
- **File-based inputs**: MPEG-TS files for testing and playback

**Output Protocols:**
- **HTSP (Home TV Streaming Protocol)**: Tvheadend's native binary protocol, optimized for efficient streaming with full metadata support
- **HTTP**: Standard HTTP streaming with support for various container formats (MPEG-TS, Matroska, MP4)
- **SAT>IP Server**: Allows Tvheadend to act as a SAT>IP server for compatible clients
- **RTSP**: Real-Time Streaming Protocol support

**Core Features:**
- **Electronic Program Guide (EPG)**: Automatic collection and management of program schedules from multiple sources (OTA, XMLTV, external grabbers)
- **Digital Video Recording**: Scheduled recordings, series recording, time-based recording, and automatic recording based on EPG data
- **Descrambling**: Support for multiple Conditional Access (CA) systems including hardware CAMs and software clients (OSCam, CCcam, etc.)
- **Multi-user support**: User authentication, access control, and per-user permissions
- **Web-based interface**: Comprehensive configuration and management through a modern web UI
- **Transcoding**: Optional on-the-fly transcoding for format conversion and bandwidth adaptation
- **Time-shifting**: Pause and rewind live TV

### 1.2 Purpose of This Document

This architecture documentation provides a comprehensive technical overview of Tvheadend's internal design and implementation. It serves as a bridge between the user-facing documentation and the source code, explaining the "why" and "how" behind the system's architecture.

The document aims to:
- Provide a high-level understanding of the system's structure and major components
- Explain the threading model and synchronization mechanisms critical to understanding the codebase
- Document the relationships and interactions between subsystems
- Identify common patterns, best practices, and potential pitfalls
- Serve as a reference for developers working on specific subsystems
- Facilitate onboarding of new contributors to the project

This is not a user manual or API reference, but rather an architectural guide for developers who need to understand, maintain, or extend the Tvheadend codebase.

### 1.3 Intended Audience

This documentation is written for:

**Primary Audience:**
- **New developers** joining the Tvheadend project who need to understand the overall architecture before diving into specific areas
- **Contributors** working on bug fixes or new features who need context about how their changes fit into the larger system
- **Maintainers** reviewing pull requests and ensuring architectural consistency

**Secondary Audience:**
- **Advanced users** interested in understanding how Tvheadend works internally
- **System integrators** building applications or services that interact with Tvheadend
- **Researchers** studying TV streaming server architectures

**Prerequisites:**
Readers should have:
- Strong C programming knowledge
- Understanding of multi-threaded programming concepts
- Familiarity with Linux system programming
- Basic knowledge of video streaming concepts (MPEG-TS, codecs, etc.)
- Experience with TV broadcasting standards (DVB, ATSC) is helpful but not required

### 1.4 How to Use This Document

This document is organized to support different reading approaches:

**For New Developers (Recommended Path):**
1. Start with [Section 1 (Introduction)](01-Introduction.md) and [Section 2 (High-Level Architecture)](02-High-Level-Architecture.md) to understand the big picture
2. Read [Section 3 (System Initialization)](03-System-Initialization.md) to understand how the system starts up
3. Study [Section 4 (Threading Model)](04-Threading-Model.md) carefully - this is critical for understanding the codebase
4. Then explore core subsystems in order:
   - [Section 5 (Input Subsystem)](05-Input-Subsystem.md) - How TV signals are received
   - [Section 6 (Service Management)](06-Service-Management.md) - How channels are managed
   - [Section 7 (Streaming Architecture)](07-Streaming-Architecture.md) - How data flows through the system
5. Dive into specific areas based on your interests:
   - [Section 8 (Profile System)](08-Profile-System.md) and [Section 9 (Muxer System)](09-Muxer-System.md) for output formatting
   - [Section 10 (Subscription System)](10-Subscription-System.md) for client connections
   - [Section 11 (Timeshift)](11-Timeshift-Support.md) and [Section 12 (DVR)](12-DVR-Subsystem.md) for recording features
   - [Section 13 (EPG)](13-EPG-Subsystem.md) for program guide data
   - [Section 14 (Descrambler)](14-Descrambler-Subsystem.md) for encrypted content
6. Review [Section 20 (Known Issues and Pitfalls)](20-Known-Issues-Pitfalls.md) to avoid common mistakes
7. Refer to [Section 21 (Development Guidelines)](21-Development-Guidelines.md) when making changes

**For Experienced Developers:**
- Use the [Table of Contents](00-TOC.md) to jump directly to relevant subsystems
- Refer to diagrams for quick visual understanding of component relationships
- Use [Section 20 (Known Issues and Pitfalls)](20-Known-Issues-Pitfalls.md) as a checklist when reviewing code
- Consult [Section 21 (Development Guidelines)](21-Development-Guidelines.md) for coding patterns and debugging techniques

**For Specific Tasks:**
- Adding a new input type → [Section 5 (Input Subsystem)](05-Input-Subsystem.md) and [Section 21 (Development Guidelines)](21-Development-Guidelines.md)
- Working on streaming → [Section 7 (Streaming Architecture)](07-Streaming-Architecture.md), [Section 8 (Profile System)](08-Profile-System.md), and [Section 10 (Subscription System)](10-Subscription-System.md)
- Recording features → [Section 11 (Timeshift)](11-Timeshift-Support.md), [Section 12 (DVR Subsystem)](12-DVR-Subsystem.md), and [Section 9 (Muxer System)](09-Muxer-System.md)
- EPG/metadata → [Section 13 (EPG Subsystem)](13-EPG-Subsystem.md)
- Encrypted channels → [Section 14 (Descrambler Subsystem)](14-Descrambler-Subsystem.md)
- Client protocols → [Section 15 (HTTP API)](15-HTTP-API-Server.md), [Section 16 (HTSP)](16-HTSP-Server.md), [Section 17 (SAT>IP)](17-SATIP-Server.md)
- Security/access → [Section 18 (Access Control System)](18-Access-Control-System.md)
- Configuration → [Section 19 (Configuration Persistence)](19-Configuration-Persistence.md)
- API development → [Section 15 (HTTP API Server)](15-HTTP-API-Server.md)
- Debugging issues → [Section 4 (Threading Model)](04-Threading-Model.md), [Section 20 (Known Issues and Pitfalls)](20-Known-Issues-Pitfalls.md), and [Section 21 (Development Guidelines)](21-Development-Guidelines.md)

**Diagrams:**
Throughout this document, you'll find Mermaid diagrams that visualize system architecture, data flow, and state machines. These diagrams are rendered in most modern Markdown viewers and can be edited directly in the source.

### 1.5 Related Documentation

**Official Tvheadend Resources:**
- **Official Website**: [https://tvheadend.org](https://tvheadend.org)
- **User Documentation**: [https://docs.tvheadend.org](https://docs.tvheadend.org)
- **GitHub Repository**: [https://github.com/tvheadend/tvheadend](https://github.com/tvheadend/tvheadend)
- **Issue Tracker**: [https://github.com/tvheadend/tvheadend/issues](https://github.com/tvheadend/tvheadend/issues)
- **Forum**: [https://tvheadend.org/projects/tvheadend/boards](https://tvheadend.org/projects/tvheadend/boards)

**Protocol and Standard References:**
- **HTSP Protocol Documentation**: Available in the Tvheadend repository under `docs/`
- **DVB Standards**: [https://www.dvb.org](https://www.dvb.org)
- **MPEG-TS Specification**: ISO/IEC 13818-1
- **SAT>IP Specification**: [https://www.satip.info](https://www.satip.info)

**Development Resources:**
- **Contributing Guide**: See `CONTRIBUTING.md` in the repository root
- **Build Instructions**: See `README.md` in the repository root
- **API Documentation**: Generated from source code comments (see `docs/class/` and `docs/property/`)

**Related Technologies:**
- **Linux DVB API**: [https://www.linuxtv.org/docs/dvbapi/](https://www.linuxtv.org/docs/dvbapi/)
- **FFmpeg/libav**: [https://ffmpeg.org/documentation.html](https://ffmpeg.org/documentation.html)
- **XMLTV**: [http://wiki.xmltv.org](http://wiki.xmltv.org)

**Note**: This architecture documentation focuses on the internal design of Tvheadend. For user-facing features, configuration options, and usage instructions, please refer to the official user documentation at [https://docs.tvheadend.org](https://docs.tvheadend.org).

---

[Table of Contents](00-TOC.md) | [Next →](02-High-Level-Architecture.md)
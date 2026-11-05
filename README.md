
# Digital Footprint Investigation

## Extracting Image and Video Metadata Using Kali Linux

### 1. Introduction
Digital images and videos contain metadata, which is hidden information describing a file. It may reveal the date and time a file was created, device information, image dimensions, GPS coordinates, file format and editing software.

Metadata analysis is useful in:
- Digital forensics and investigations.
- Identifying the source of digital files.
- Investigating suspicious images and videos.
- Establishing file timelines.
- Identifying privacy leaks.
- Understanding digital footprints.

### 2. Objectives
- Install and use ExifTool in Kali Linux.
- Extract metadata from JPEG and PNG images.
- Investigate GPS location information.
- Extract metadata from MP4 videos.
- Save metadata investigation results.
- Calculate SHA-256 hashes.
- Understand security and privacy risks associated with metadata.

### 3. Tools and Requirements
- Kali Linux
- Terminal
- ExifTool
- Two JPEG/JPG photographs.
- One PNG image.
- One MP4 video.

### 4. Repository Structure

```text
Digital-Footprint-Investigation/
│
├── README.md
├── img/
│   ├── photo1.jpg
│   ├── photo2.jpg
│   └── sample.png
│
├── videos/
│   └── video.mp4
│
|
│── photo1_metadata.txt
│── video_metadata.txt
│
└── screenshots/
```

### 5. Installing ExifTool

Update Kali Linux:

```bash
sudo apt update
```

Install ExifTool:

```bash
sudo apt install libimage-exiftool-perl -y
```

Verify installation:

```bash
exiftool -ver
```

### 6. Preparing the Working Directory

Create the working directory:

```bash
mkdir Metadata_Lab
cd Metadata_Lab
```

Check available files:

```bash
ls -lh
```

### 7. Identifying File Types

Run:

```bash
file *
```

The command helps identify the actual file formats.

File types to identify:
- JPEG images.
- PNG image.
- MP4 video.

Identifying the actual file type is important because file extensions can be changed or misleading.

### 8. Extracting Image Metadata

Examine the first JPEG image:

```bash
exiftool photo1.jpg
```

Examine the second JPEG:

```bash
exiftool photo2.jpg
```

Examine the PNG image:

```bash
exiftool sample.png
```

Important metadata fields include:

- Make – Camera or phone manufacturer.
- Model – Device model.
- DateTimeOriginal – Date and time the picture was taken.
- GPSLatitude – GPS latitude.
- GPSLongitude – GPS longitude.
- ImageWidth – Image width.
- ImageHeight – Image height.
- Software – Editing software.
- FileType – File format.

Not every image contains all metadata fields.

### 9. GPS Metadata Investigation

Check GPS information:

```bash
exiftool -gps:all photo1.jpg
```

Display GPS coordinates numerically:

```bash
exiftool -n -GPSLatitude -GPSLongitude photo1.jpg
```

GPS metadata may reveal the location where a photograph was taken.

Security implications:
- Attackers may identify someone's location.
- Sensitive workplace locations may be exposed.
- Organizations may unintentionally leak information when publishing photographs online.

### 10. Extracting Video Metadata

Examine the MP4 video:

```bash
exiftool video.mp4
```

Look for:
- Video creation date.
- Duration.
- Video dimensions.
- Frame rate.
- Video codec.
- Audio information.
- Device or software information.

Display selected video properties:

```bash
exiftool -Duration -ImageWidth -ImageHeight -VideoFrameRate video.mp4
```

Examine timestamps:

```bash
exiftool -time:all -a -G1 video.mp4
```

### 11. Saving Metadata Results

Export image metadata:

```bash
exiftool photo1.jpg > photo1_metadata.txt
```

Export video metadata:

```bash
exiftool video.mp4 > video_metadata.txt
```

Confirm that the reports were created:

```bash
ls -lh *.txt
```

View the reports:

```bash
cat photo1_metadata.txt
cat video_metadata.txt
```

### 12. File Integrity Verification

Calculate SHA-256 hashes:

```bash
sha256sum photo1.jpg photo2.jpg sample.png video.mp4
```

SHA-256 hashes help identify changes to files and support file integrity verification.

### 13. Metadata Removal

Create a copy of the image without metadata where supported:

```bash
exiftool -all= -o img/cleaned_photo.jpg img/photo1.jpg
```

Compare the original and cleaned images:

```bash
exiftool photo1.jpg
exiftool cleaned_photo.jpg
```

The original file remains unchanged. Always preserve original evidence during forensic investigations.

### 14. Practical Deliverables

The practical report should contain:

1. Introduction – Brief explanation of metadata.
2. Installation – Screenshot showing ExifTool installation/version.
3. Image Analysis – Findings from two JPEG images.
4. PNG Analysis – Findings from one PNG image.
5. GPS Investigation – GPS findings or evidence of absent GPS metadata.
6. Video Analysis – Findings from one MP4 video.
7. File Integrity – SHA-256 hash values.
8. Reflection – Security and privacy implications.

Include screenshots of commands and their outputs. Redact private GPS coordinates before publishing.

### 15. Case Study: Server Room Photograph

An employee working in a financial institution takes a photograph inside the organization's server room and shares it on social media. The photograph contains GPS coordinates, device information and the date it was taken.

Discussion questions:

### 1. What information could a malicious actor obtain from the photograph?

A malicious actor could obtain:

- GPS coordinates: The exact location of the server room.
- Device information: The camera or phone manufacturer and model.
- Date and time: When the photograph was taken.
- Software information: Applications used to edit the photograph.
- Visual information: Details of servers, network equipment and the organization's internal environment.

### 2. How could this information assist an attacker during reconnaissance?

- Identify the organization's physical location.
- Determine when employees are present.
- Identify the types of devices and equipment used.
- Study the organization's server room environment.
- Plan physical attacks, social engineering, or targeted cyberattacks.

### 3. What privacy and organizational security risks arise?

- Exposure of sensitive workplace locations.
- Unauthorized access to organizational facilities.
- Employee privacy violations.
- Leakage of confidential organizational information.
- Increased risk of targeted cyberattacks.
- Damage to the organization's reputation.

### 4. What measures should the organization implement to prevent metadata leakage?

- Remove GPS information and sensitive metadata before sharing photographs.
- Train employees on digital privacy and cybersecurity.
- Establish policies governing photography in sensitive areas.
- Restrict photography inside server rooms.
- Inspect files before publishing them online.
- Use security awareness programs to educate employees about metadata risks.

### 16. Key Lessons

- Digital Footprint: Files can reveal information beyond what is visible to the human eye.
- Digital Forensics: Metadata supports investigations but can be modified and should not automatically be treated as conclusive evidence.
- Privacy Protection: Individuals and organizations should inspect and remove sensitive metadata where appropriate before publishing files.
- Evidence Preservation: Original files should be preserved, and investigations should be performed on copies.

### 17. Reference

ExifTool Official Website: https://exiftool.org/

syncrecover

A Fish shell function wrapping rsync for fault-tolerant data recovery transfers from Linux (ext4) partitions to portable exFAT drives. By default, it transfers all files and directories, or you can pass specific file extensions on the command line to selectively extract only the file types you need (case-insensitively).

Features

• Copy Everything or Filter on the Fly: Transfers all files by default, or dynamically builds case-insensitive --include rules when you pass extensions as arguments (e.g., doc pdf zip).

• Built-In Recovery Preset (--preset): Includes a one-flag preset for common documents, spreadsheets, presentations, audio, images, and archives (.m4a, .doc, .docx, .xls, .xlsx, .ppt, .pptx, .bmp, .gif, .rtf, .csv, .zip, .7z).

• Clean Destination Structure (--prune-empty-dirs): Automatically omits empty directories when filtering for specific file types.

• exFAT-Optimized Flags (-rth --modify-window=2 --no-links): Handles exFAT's 2-second timestamp resolution, skips unsupported Linux symlinks, and prevents cross-filesystem permission errors.

• Fault-Tolerant Recovery (--ignore-errors + sudo): Continues transferring readable files even if damaged sectors or restricted permissions are encountered on the source partition.

• Accurate Progress Tracking (--no-inc-recursive): Performs a full upfront file scan so the progress percentage climbs steadily from 0% to 100% without jumping backward.

• Pinned Disk Space Monitor: Uses tput cursor positioning to pin a live timestamp and df -h readout for your destination drive at the top of the terminal, refreshing every 30 seconds.

• Safe RAM Cache Flushing (sync): Ensures all buffered writes in system memory are flushed to the exFAT drive before signaling completion.

• Self-Cleaning Error Log: Saves any skipped files or read/write errors to ~/skipped_recovery_files.txt and automatically deletes the file if zero errors occurred.

Requirements

• Fish Shell (fish)

• rsync (v3.1.0+ for --info=progress2 support)

• sudo privileges (to read protected directories on recovered ext4 partitions)

• ncurses (tput, pre-installed on most Linux systems)

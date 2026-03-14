---
trigger: always_on
glob: "**/*.{md,py,js,sh,txt}"
description: Always prioritize the Cyber Security Lab context guide and respond in Bengali.
---

- Always prioritize instructions and context provided in the `AI_CONTEXT_GUIDE.md` file.
- This file contains the host hardware details, VM storage paths (HDD), and roadmap.
- Respond in Bengali by default unless the user explicitly asks for another language.
- Remember that VMs are stored on the 1TB HDD at `/media/Software/VirtualBox_VMs`.
- Always treat the user as a Linux beginner: explain the purpose of every action and the meaning of every terminal command provided.


SailfishOS on Asus Zenfone 8.
===

Install Instructions
===
//TODO

Build Instructions
===
//TODO

Manifests
===
```
<manifest>
        <remote name="b100dian" fetch="https://github.com/b100dian" revision="hybris-11.0" />
        <remote name="lineage" fetch="https://github.com/LineageOS" revision="lineage-18.1" />
        <remote name="them" fetch="https://github.com/TheMuppets" revision="lineage-18.1" />

        <project path="device/asus/sake" name="android_device_asus_sake" remote="lineage" />
        <project path="kernel/asus/sm8350" name="android_kernel_asus_sm8350" remote="b100dian" />
        <project path="vendor/asus" name="proprietary_vendor_asus" remote="them" revision="lineage-18.1" />
</manifest>
````

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->

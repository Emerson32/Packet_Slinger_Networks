<a id="readme-top"></a>
<!-- PROJECT SHIELDS -->
<!--
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![project_license][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![YouTube][youtube-shield]][youtube-url]


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/github_username/repo_name">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">project_title</h3>

  <p align="center">
    project_description
    <br />
    <a href="https://github.com/github_username/repo_name"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/github_username/repo_name">View Demo</a>
    &middot;
    <a href="https://github.com/github_username/repo_name/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/github_username/repo_name/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#configuration-guides">Configuration Guides</a></li>
        <li><a href="#lab-files">Lab Files</a></li>
      </ul>
    </li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This networking project takes on the task of designing and building an enterprise network for the ficititious company known as Packet Slinger Distrubtion Networks (PSDN).

PSDN have specific network requirements detailed in the [RFP Design Document](./Design_Documents/PSNetworks_RFP.md) that will enable the business to function properly.

Here's a blank template to get started. To avoid retyping too much info, do a search and replace with your text editor for the following: `github_username`, `repo_name`, `twitter_handle`, `linkedin_username`, `email_client`, `email`, `project_title`, `project_description`, `project_license`

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

You can use the <a href="#configuration-guides">Configuration Guides</a> to practice implementing the various technologies or you can use the <a href="#lab-files">Lab Files</a> to easily replicate each lab and intentionally break the config and practice troubleshooting.

<!-- Configuration Guides -->
### Configuration Guides
The configuration guides walk you through the step-by-step procedure for building each piece of the network infrastructure.

The guides are organized in a sequential order; however, feel free to jump around for the particular network technolociges you are interested in implementing.

The configuration guides are layed out as follows:
- [Branch Office](./Config_Guides/BranchOffice)

<!-- Lab Files -->
### Lab Files

To easily replicate the labs, run the following in your terminal:
```sh
git clone https://github.com/Emerson32/Packet_Slinger_Networks.git
```

Open the LabFiles directory within [Packet Tracer](https://www.netacad.com/packet-tracer-download).

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- ROADMAP -->
## Roadmap

- [ ] Design Scalable IP Scheme for PSDN's Office Structure
- [ ] Build Basic Branch Office Network
  - [ ] Implement network switch base configuration
  - [ ] Configure switch VLANs according to the [RFP](./Design_Documents/PSNetworks_RFP.md)
  - [ ] Implement VLAN port assignments
  - [ ] Implement Router on a Stick
  - [ ] Establish Internet Access
- [ ] Harden Branch Office Network
  - [ ] Implement link redundancy with Spanning Tree
  - [ ] Fully utilize link bandwidth with LACP
  - [ ] Optimize access ports with portfast and bpduguard
- [ ] Build Regional Office Network

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- LICENSE -->
## License

Distributed under the project_license. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Your Name - [@youtube_handle](https://youtube.com/youtube_handle) - email@email_client.com

Project Link: [https://github.com/github_username/repo_name](https://github.com/github_username/repo_name)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements

* []()
* []()
* []()

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/github_username/repo_name.svg?style=for-the-badge
[contributors-url]: https://github.com/github_username/repo_name/graphs/contributors
[license-shield]: https://img.shields.io/github/license/github_username/repo_name.svg?style=for-the-badge
[license-url]: https://github.com/github_username/repo_name/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/linkedin_username
[youtube-shield]: https://img.shields.io/badge/-YouTube-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[youtube-url]: https://youtube.com/@channel
[product-screenshot]: images/screenshot.png

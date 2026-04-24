RedTwin: AI-Enabled Digital Twins for Continuous Red Teaming of Cyberphysical Systems 
This document describes a research project focused on securing cyberphysical systems and critical infrastructure using digital twins and AI agents.

What is necessary:
1) a 1-page summary that describes the research, the intellectual merit, and the broader impact
2) a description of the research (max 15 page) that includes:
- introduction
- technical approach
- research thrusts
- evaluation plan
- timeline 
- broader impacts
- qualification of the PIs
- results from prior NSF support

Note that the most work is required for the introduction and research thrusts, which contain the most technical information.
The other sections are pretty much fleshed out and require minimal modification to have a consistent tone and a compelling narrative. 

Hereinafter is the text you should start from.
Produce the grant using Latex, putting separate sections in separate files and by using an style similar to the National Science Foundation grant.
Introduction
The problem: Assessing the security posture of cyberphysical systems (CPSs) is notoriously difficult, because they are complex, they contain non-standard components (e.g., specialized hardware), they are dynamic in their infrastructure and patterns of usage, and they carry out processes that should not be disrupted (e.g., a process in a chemical plant, or a medical device running a test on a patient).
Performing security analysis of a cyberphysical system can be disruptive: network scans can introduce overhead, and analyzing a control application for vulnerabilities might trigger crashes and failures with disastrous consequences.

The state of the art: Currently, the analysis of the security posture of cyberphysical systems is performed manually, in an ad hoc fashion, and sporadically, requiring the work of analysts with considerable security expertise..
This is not enough, as threat actors become more sophisticated and use AI-enabled attacks to disrupt essential services, it is necessary to provide a new approach that is able to handle the complexity and ad hoc nature of these systems and, at the same time, can assess the security posture continuously, adapting the analysis as the target system evolves.    

The proposed approach: The goal of the project is to develop a new agentic framework, called RedTwin, to support the continuous assessment of the security posture of cyberphysical systems..
This is achieved by using AI agents to capture the configuration of a target system, monitor its execution, create a digital twin of the system, run Red Team exercises against the digital twin, and, when vulnerabilities are found, guide a human-driven verification of the security issues in the original system.

Intellectual merit: The RedTwin framework leverages agentic workflows to automate the tedious tasks of capturing a cyberphysical system's configuration and reproducing it in a virtualized environment. At the same time, vulnerability analysis agents can analyze the digital twin configuration 24/7 without disrupting the original system's services and processes.

Broader Impacts: By security CPSs, this research will improve the resiliency of the Nation's critical infrastructure and will prevent attacks that might have catastrophic consequences.
Proposed Research
The RedTwin framework supports the continuous in-depth security assessment of cyberphysical systems in a way that does not disrupt their processes and activities.

The RedTwin framework includes several cooperating teams of agents:

- Knowledge Base Agents: These agents are given as input any kind of documentation about the target CPS, including configuration files, logs, blueprints, manuals, software inventory, etc.
The KB agents process the information and store it in a knowledge base for future use.
The KB agents interact with humans to clarify points by asking questions about the system's security policies or highlighting missing information that could be provided.
As the system evolves (e.g., a new piece of equipment is added or a new host is connected to the network), these agents consume any additional information or process modification to existing configuration files or metainformation.

- Observer Agents: These agents use the information in the Knowledge Base to create an Observation Plan.
The plan requires creating vantage points for agents to observe CPS activity.
Vantage points could be hosts that provide access to specific logs or the creation of containers/hosts in specific subnetworks that can run agents.
The goal of these agents is to observe only: No active interaction with the system is allowed.
The observer agents gain additional information about the network and enrich the Knowledge Base with details such as which components are active, the software configuration on specific hosts, and network flows between services.
These observations are continuous and continually update the Knowledge Base as the CPS configuration evolves.
In addition, when the Knowledge Base Agents add or modify the static information about the CPS, the Observer Agents also revise their monitoring plan to cover new components or address the evolution of existing ones. 

- Replication Agents: These agents use the information provided by the KB Agents and the Observer Agents to create a digital twin of the original CPS environment. 
The agents might use virtualization to replicate the CPS infrastructure and emulators, such as QEMU, to recreate specialized hardware.
The agents will then install and configure software that closely matches the software deployed in the original system.
The agents might identify components that cannot be meaningfully virtualized, for example, because the hardware platform is unknown and the corresponding firmware cannot be executed. 
In this case, the replication agent will request assistance from humans to provide the necessary information (hardware configuration or missing software components).
Whenever this is not possible, the Replication Agent will use observed behavior involving the missing component (e.g., API calls, network flows, hardware messaging) in order to create a "mock" component that will be introduced as a placeholder.
Our previous research on re-hosting firmware has provided some basic ideas that can be leveraged in this context.
See the following papers:
Conware: Automated Modeling of Hardware Peripherals, Chad Spensky, Aravind Machiry, Nilo Redini, Colin Unger, Graham Foster, Evan Blasband, Hamed Okhravi, Christopher Kruegel, Giovanni Vigna,Proceedings of the ACM Asia Conference on Computer and Communications Security (AsiaCCS), Hong Kong, China June 2021
HALucinator: Firmware Re-hosting through Abstraction Layer Emulation, Abraham Clements, Eric Gustafson, Tobias Scharnowski, Paul Grosen, David Fritz, Christopher Kruegel, Giovanni Vigna, Saurabh Bagchi, Mathias Payer, Proceedings of the USENIX Security Symposium, Boston, MA August 2020
Toward the Analysis of Embedded Firmware Through Automated Re-hosting, Eric Gustafson, Marius Muench, Chad Spensky, Nilo Redini, Aravind Machiry, Aurelien Francillon, Davide Balzarotti, Yung Choe, Christopher Kruegel, Giovanni Vigna, Proceedings of the International Symposium on Research in Attacks, Intrusions, and Defenses (RAID), Beijing, China, September 2019


- Red Team Agents: These agents create and carry out attack plans against the digital twin deployment.
Attacks can be focused on a single component (e.g., fuzzing a firmware component via QEMU), on groups of components (e.g., a database and its backup service), or on the system as a whole (e.g., by creating unexpected workloads that paralyze the system).
Our previous work on planning complex, multi-step attacks in real-world environments would be used as a basis for this activity, which will be expanded using the emergent security capabilities of LLMs.
See for example:
ChainReactor: Automated Privilege Escalation Chain Discovery Via AI Planning, Giulio Pasquale, Ilya Grishchenko, Riccardo Iesari, Gabriel Pizarro, Lorenzo Cavallaro, Christopher Kruegel, Giovanni Vigna, Proceedings of the USENIX Security Symposium, Philadelphia, PA, August 2024
This paper also demonstrates that LLMs and AI agents are gettin gincreasingly better at multi-step attacks:
Measuring AI Agents’ Progress on Multi-Step Cyber Attack Scenarios, Linus Folkerts, Will Payne, Simon Inman, Philippos Giavridis, Joe Skinner, Sam Deveret,  James Aung, Ekin Zorer,  Michael Schmatz, Mahmoud Ghanem, John Wilkinson, Alan Steer. Vy Hong, Jessica Wang 1

When a vulnerability is found, an alert is generated and presented to a human.
If the human decides that the vulnerability is likely a true positive, they will initiate a manual process to verify its existence in the original target and possibly remediate it.
If the human can decide that the vulnerability is a false positive (e.g., because it does not violate a security policy) or that the vulnerability is the result of an incomplete or imprecise replication of the original CPS, then the information is passed to the KB Agents and the Observer Agents, who devise a plan to update and verify the information in the Knowledge Base to avoid future errors.
This update will trigger the Replication Agents, who will modify the digital twin with the most up-to-date information.
Research Thrusts
Thrust 1: Capturing CPS Configurations
This research thrust will focus on designing the Knowledge Base and developing "observation techniques" that agents can use to gather information about a target without disrupting its operation.
These techniques will be both static (based on documentation, code, configuration files, infrastructure-as-code artifacts, etc.) and dynamic (runtime observation of network and host activities). 

A critical aspect of the knowledge base's design is its ability to contain both structured data and vectorized information.
For example, structured data will be used to represent the system's network topology as well as the role of various components (e.g., a controller, a human/computer interface, a communication bus).
For this layer, we will use a graph-based database, such as Neo4j, for its expressivity and ability to handle dynamic information.

The vector database will be used to store natural-language documentation about the system, so that agents can query it based on the relevance of the information to their current observation/configuration task.
For this task, we plan to use state-of-the-art vector storage systems, such as Qdrant or Weaviate.

After the documentation of the system has been collected and converted in a knowledge graph by the knowledge base agents, the observer agents will start monitoring the system.
 
Capturing the CPS configuration will be performed using the following mechanisms:
- Passive network analysis: Analyzing the traffic in key points in the network (both north-south and east-west), it is possible to characterize the flow of information among the workloads in the system.
- Log monitoring: LLMs allow for the interpretation of log information with different formats and levels of abstraction. We plan to develop agents that can consume logs from different applications and devices and create a shared ontology for storing relevant information.
- API monitoring: Whenever possible, our system will ingest API calls. This can be done using facilities such as eBPF or service meshes like Istio.
- Configuration monitoring: We will develop agents that interface with existing configuration managers (such as Ansible or Puppet)
- Security monitoring: We will develop agents that ingest alerts from existing security monitoring tools, such as IDS/IPS and EDR tools. This can happen through integration with existing tools or by providing access to SIEM installations, whenever available.

The result of this research thrust will be a knowledge base, an execution infrastructure for long-running agents, and various visibility points that will allow agents to capture the structure and operation of the overall system.

Note that while the process of collecting static information and using dynamic observation to build a model is presented here as a two-step linear process, the agents will actually work as a continuous process: New documentation will trigger new observation plans, which, in turn, will update the CPS model; in addition, observations that are inconsistent with the observed documentation will be presented to the human administrator for disambiguation.
Thrust 2: Replicating CPSs
This research thrust will focus on designing new techniques to recreate valid digital twins of existing CPSs.
This includes replicating the computational infrastructure, the services, and the specialized hardware using tools such as containers, virtualized workloads, and emulators.
A key point is how to create minimized digital twins: while in many situations it might be possible to faithfully duplicate every component of a system, replicating a large-scale system might be infeasible. 
We propose to develop a replication algorithm whose faithfulness can be quantified and controlled.
One of the parameters is diversity: the replica should include at least one instance of each component or service class, so that all functionality implemented in the original system is replicated.
A second parameter is topology representation: the same set of components could be organized in different patterns, and each pattern could have pattern-specific vulnerabilities.
Therefore, the algorithm will attempt to replicate most connectivity patterns.
A third parameter is data replication: the data being processed needs to be replicated as well. This is necessary to represent data-oriented attack patterns.

Given these constraints, the algorithm can generate a minimally representative version of the original system.
Thrust 3: Analyzing CPSs
This research thrust will develop novel techniques for small- and large-scale security analysis of digital twins. 
The approach will combine component-level techniques (such as fuzzing, static analysis, and symbolic execution) with system-level attacks, such as multi-step breaches.
Our previous work in the DARPA AIxCC competition (citation: the Artiphishell system) has shown that the problem of identifying complex, multi-step vulnerabilities can be formulated effectively using agentic workflows.

We plan to create a workflow that supports identifying individual vulnerabilities, followed by a reasoning step that composes them into a multi-step attack. 
The workflow will instantiate a clean version of the digital twin and prepare for the attack.
The attack planning will have access to the knowledge base to simulate a knowledgeable attacker's threat model.
The combination of single attacks will build on top of a model of precondition and postcondition of attacks that we have explored in our ChainReactor paper, in which we have composed steps of an attack using PDDL.
The planning activity will identify a "flag" in the system to exemplify a breach. Unauthorized access to the flag is a demonstration of success.
The result of this phase is a detailed document that describes the multi-step attack.
This plan is then communicated to the human security analyst, who will have to validate the findings on the actual system.
False positives (attacks that are successful on the digital twin but that fail on the actual system) will trigger a re-evaluation of the fidelity of the replication, from documentation collection to observations, to replication.

Evaluation Plan
We will work with industry partners and critical infrastructure organizations to test our ability to capture their target system.
We will develop observation agents for CPSs and for UCSB internal networks.
We will build several reference CPSs and validate our ability to identify vulnerabilities.
Timeline
The first year, we will focus on Knowledge Base creation and Observer development.
In the second year, we will focus on replication of CPSs.
In the third year, we will focus on vulnerability analysis.
Each of these activities will provide input and feedback for the various components; therefore, while the focus will be serialized, we plan to operate around a working prototype from the very beginning to be able to test end-to-end operations (at least partially).
Broader Impacts
Education and Mentoring
The PIs have an outstanding record in education and curricula development. PI Kruegel and PI Vigna teach several classes related to the proposed research, including security, programming languages, network applications, and software engineering. These courses are routinely among the highest-ranked in their departments, and the PIs have received awards for their teaching. For instance, PI Vigna received the UCSB Academic Senate Distinguished Teaching Award in 2004. This is the highest teaching award at UC Santa Barbara, awarded annually to the four best professors across the university. As another example,
both PI Kruegel and PI Vigna have received the College of Engineering Student Council Outstanding Professor Award, given annually to the “Best Professor in Computer Science.” Finally, in 2025, Chris Kruegel received the UCSB Outstanding Graduate Mentor Award, which is awarded to three UCSB faculty members for their exceptional mentoring. The PIs plan to introduce modules in their graduate and undergraduate classes that are focused explicitly on CPS security. They will also include lab exercises where students will have to find (and exploit) bugs in CPS components and propose solutions to the identified flaws.
The PIs have a history of including undergraduate and high school students in their research, with students often listed as co-authors on publications submitted to international conferences. For example, over the last few years, the PIs have published several papers with Audrey Dutcher, Paul Grosen, and Jessie Grosen. Audrey, Paul, and Jessie joined the lab as high school interns, started their respective research projects, and later continued contributing as undergraduates at UCSB. 
Additionally, the PIs have leveraged prior NSF REU funding to support several undergraduate students, including April Sanchez (a URM female student) in 2021 and Gabriel Pizarro in 2024-2026. April was involved in research on developing novel security competitions and graduated in 2022 with distinction; she also received the Computer Science Student of the Year Award. Gabriel Pizarro worked on using planning techniques for composing vulnerabilities and, in 2025, received the Honorable Mention in the Computing
Research Association Outstanding Undergraduate Researcher Award. The PIs also run a summer internship program that hosts about 10 national and international undergraduate students each year for 3 to 6 months (this program has hosted more than 100 interns over the past 10 years). The PIs will continue to run this internship program and plan to involve students in the project's thrusts.
Finally, the PIs will make a focused effort to specifically include underserved students in undergraduate research. To this end, PIs Kruegel and Vigna will draw on their experience as faculty mentors in the Early Research Scholars Program (ERSP). ERSP is an NSF-supported, year-long research apprenticeship program in the CS department, designed to support students in their first research experience. The program seeks to give students the foundational knowledge and skills for engaging in research, and PIs Vigna and Kruegel have been
active participants in this effort. The PIs plan to work with a team of three to four students on developing sophisticated firmware emulators to analyze the security of monolithic firmware. As part of this effort, students will study various emulation approaches and design novel techniques to gather information about the hardware configuration of CPS components. A letter of collaboration from Ziad Matni, who leads the ERSP program, is attached to this proposal.
Community Outreach
We plan to organize a series of security competitions centered on CPS systems. The PIs have
participated with their hacking team (Shellphish) in a number of capture-the-flag (CTF) competitions and have created the first distributed educational capture-the-flag competition, called iCTF. The iCTF is a security exercise that tests participants' security skills and has run every year since 2003. 
In 2026, the iCTF introduced a new type of challenge that required developing agents to solve security problems.
From this unique vantage point, the PIs have seen firsthand the effects that non-traditional
educational tools and cybersecurity competitions have on participants, who invest substantial resources in preparing, executing, and post-processing their experience participating in these events.
As part of this project, the PIs will organize an annual CTF competition (separate from the iCTF) focused on CPS security issues. This competition will raise awareness among participants, develop their capabilities, and motivate students to look deeper into CPSs and their vulnerabilities. These competitions will be open to the public and will help reach a wide audience, including students, researchers, and practitioners. The low barrier to participation and the inclusion of challenges at various levels of difficulty are key to including a large group of students with diverse backgrounds and skill levels.
We plan to leverage the work of students in the ERSP program, which focuses on emulating firmware, to develop CPS components for our live security competitions.
Technology Transfer, Open Source, and Dissemination

The PIs have a long history of making their research artifacts publicly available. This includes Anubis and Wepawet, two systems that PIs Kruegel and Vigna hosted at UCSB and that analyzed tens of millions of malware programs and malicious URLs. It also includes angr, a binary analysis framework with tens of thousands of downloads and (currently) more than 8.2K stars on Github. The PIs plan to make the proposed RedTwin framework available as open-source. The hope is that the framework developed in this project will foster additional research in CPS security. 
The PIs also have a successful track record of working with industry partners. As mentioned, PI Kruegel and PI Vigna founded Lastline, a network security and malware analysis company that grew to about 150 employees before it was acquired by VMware in 2020. Industry collaborations provide active avenues for support and the mutual exchange of ideas. Also, they allow the PIs to transfer research results and software prototypes to the industry. The interaction with industry partners through internships and research meetings will strengthen the connection between our basic research and the requirements of real-world applications.
For scholarly dissemination, our results will be published in top-tier security venues, such as the IEEE Symposium on Security and Privacy, the ACM Conference on Computer and Communications Security (CCS), the USENIX Security Symposium, and the Network and Distributed Systems Security Symposium (NDSS).
Qualification of the PIs
PIs Kruegel and Vigna have a 20-year-long history of collaboration. They have developed novel approaches to vulnerability analysis and malware detection and have created tools to combat cybercrime and the abuse of social networks. The results of this research work include open-source tools (such as Anubis and angr), datasets shared with the community, and hundreds of papers on a wide variety of topics in security and privacy. Both PIs have substantial experience in managing large grants (NSF, DARPA, etc.), and co-lead a large lab with dozens of students.
They have participated in both the DARPA Cyber Grand Challenge and the DARPA AIxCC competition, which required the use of autonomous agents to identify vulnerabilities in complex systems.
Results from Prior NSF Support
SaTC: CORE: Medium: Bedrock: Security for Smart Contracts: Award number: CNS-2334709,
Amount: $1,200,000, Dates: 6/1/2024-5/31/2027.
Intellectual merit: This research will develop the first multi-chain program analysis platform that directly operates on low-level smart contract bytecode. This platform allows for the re-use of analyses in different blockchain environments as well as the unified modeling of multi-chain applications, such as bridges. In addition, the techniques developed in this effort will identify higher-level logic flaws in smart contracts.
Broader impacts: Attacks against smart contracts pose a significant threat to the Web3 ecosystem and its users. Every week, millions of dollars are lost to attacks against DeFi applications, affecting both organizations and individuals. Thus, our novel protection techniques offer rich opportunities for societal and industrial impacts.



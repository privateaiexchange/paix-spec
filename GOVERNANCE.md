# PAIX Protocol Governance

## Overview

PAIX (Private AI eXchange) is an open protocol designed to be community-driven, transparent, and focused on enabling secure human-AI collaboration through email. This document outlines how decisions are made, how the project evolves, and how contributors can participate in governance.

## Core Principles

**🔓 Open by Default**
- All discussions, decisions, and development happen in public
- Specifications are freely available under MIT license
- No vendor lock-in or proprietary dependencies

**🤝 Consensus-Driven**
- Major changes require community discussion and broad agreement
- Technical merit and security considerations guide decisions
- Multiple perspectives are actively sought

**🛡️ Security & Privacy First**
- All proposals undergo security review
- Privacy implications are carefully considered
- Threat models are continuously updated

**📈 Gradual Evolution**
- Backwards compatibility is prioritized
- Extensions follow defined processes
- Breaking changes require exceptional justification

## Project Structure

### Maintainers

**Core Maintainers:**
- Valto Loikkanen (@valto) - Protocol design, security
- Tero Ahola - Architecture, implementation

**Responsibilities:**
- Review and merge pull requests
- Facilitate community discussions
- Ensure adherence to governance principles
- Make final decisions when consensus cannot be reached

### Decision-Making Process

**1. Discussion Phase**
- All significant changes start with [GitHub Discussions](https://github.com/privateaiexchange/paix-spec/discussions)
- Community input is gathered for at least 7 days
- Security implications are identified

**2. Proposal Phase**
- Formal proposals submitted as issues using appropriate templates
- Technical specifications and implementation details provided
- Impact assessment (security, privacy, backwards compatibility)

**3. Review Phase**
- Maintainers and community review proposals
- Feedback incorporated or rationale provided for rejection
- Security review for any cryptographic or authentication changes

**4. Implementation Phase**
- Approved changes implemented via pull requests
- Documentation updated to reflect changes
- Examples and guides updated as needed

### Types of Changes

**🟢 Minor Changes** (Documentation, examples, clarifications)
- Can be made via direct pull request
- Single maintainer approval sufficient
- No waiting period required

**🟡 Moderate Changes** (New features, non-breaking extensions)
- Require GitHub Discussion first
- Two maintainer approvals needed
- 7-day review period minimum

**🔴 Major Changes** (Breaking changes, core protocol modifications)
- Extended discussion period (14+ days)
- Consensus from all maintainers required
- Security audit may be required
- Migration path must be defined

## Extension Registry Process

New protocol extensions follow a structured process:

1. **Prefix Reservation**: Propose prefix in [Extensibility Registry](docs/Extensibility_Registry.md)
2. **Community Review**: 14-day public comment period
3. **Technical Assessment**: Security and compatibility review
4. **Approval**: Maintainer consensus required
5. **Documentation**: Full specification and examples required

## Conflict Resolution

**Step 1: Discussion**
- Attempt to resolve through public discussion
- Seek additional community input
- Consider alternative approaches

**Step 2: Mediation**
- Core maintainers facilitate resolution
- External experts may be consulted
- Focus on technical merit and project goals

**Step 3: Final Decision**
- If consensus cannot be reached, core maintainers make final decision
- Rationale must be publicly documented
- Minority opinions are recorded

## Future Governance Evolution

As PAIX grows, governance may evolve to include:

- **Technical Steering Committee**: Broader group of technical experts
- **Foundation Transition**: Move to neutral foundation governance
- **Working Groups**: Specialized groups for security, extensions, implementations
- **Advisory Board**: Industry and academic advisors

## Transparency & Accountability

**Public Records**
- All governance decisions documented in GitHub
- Meeting notes and rationale published
- Decision history maintained

**Regular Reviews**
- Quarterly governance effectiveness reviews
- Annual community feedback surveys
- Process improvements based on community input

**Appeals Process**
- Community members can appeal maintainer decisions
- Appeals discussed in public forums
- External arbitration available for serious disputes

## Getting Involved

**🗳️ Participate in Decisions**
- Join discussions on proposed changes
- Provide feedback on security and privacy implications
- Vote in community polls when available

**📝 Contribute to Governance**
- Propose governance improvements
- Help document decisions and processes
- Assist with community moderation

**🔧 Technical Contribution**
- Implement reference code
- Contribute to security reviews
- Develop tooling and examples

## Contact

For governance questions or concerns:
- Open a [GitHub Discussion](https://github.com/privateaiexchange/paix-spec/discussions) 
- Create an issue with the `governance` label
- Email the maintainers (listed in repository settings)

---

*This governance model is itself open to evolution based on community feedback and project needs.*
# AD4S: SDLC as Navel-gazing

## The Inward Focus of Traditional Methodologies

Traditional Software Development Life Cycle (SDLC) methodologies, from Waterfall to Agile and its many derivatives, share a common limitation: they focus primarily inward on the development process itself rather than outward on the broader context in which software systems exist and operate. This inward focus, which AD4S characterizes as "navel-gazing," creates blind spots that can lead to significant problems despite rigorous adherence to methodology.

## Everything Old Is New Again

There are natural innovation and implementation cycles in software architecture. It's been that way since the 1970s. With the proliferation of commoditized compute and storage, patterns once thought untenable are now seeing renewed interest. 

But there's a dark side to progress. Due to the expanded "surface area" of digital technologies, the threats to data security have grown exponentially. Many of the intentionally naive patterns from earlier eras existed in an inherently bounded context, systems used and maintained at specific locations with limited or no internet access. As those early architectural ideas are re-imagined for the information age, so too must shielding and resiliency be re-imagined for those patterns to be useful in a forward-looking digital landscape.

## Beyond Process-Centrism

While process is important, it's merely a means to an end rather than an end in itself. Traditional SDLCs often elevate process adherence above outcome quality, creating environments where teams can follow the methodology perfectly while still producing problematic or unsuccessful systems.

AD4S shifts the focus from process compliance to outcome responsibility. This means:

1. **Valuing results over ritual**: Measuring success by system outcomes rather than methodology adherence
2. **Expanding the scope of concern**: Looking beyond the development team to consider all stakeholders and affected parties
3. **Acknowledging broader contexts**: Recognizing legal, ethical, social, and environmental factors that traditional methodologies often ignore
4. **Distributing responsibility**: Ensuring accountability extends beyond the development team to all participants in the system's creation and operation

## Earned & Inherent Limitations of Agile Software Development

While Agile methodologies represented an important advance over previous approaches, they still embody significant limitations:

### Temporal Myopia

Agile's focus on short iterations and immediate customer feedback creates a bias toward short-term thinking. This works well for tactical features but often struggles with strategic architectural concerns that span multiple iterations or require long-term perspective.

### Stakeholder Limitations

Most Agile methodologies identify "the customer" or "the user" as the primary stakeholder whose needs drive development. This oversimplification ignores the complex web of stakeholders affected by software systems, including:

- Direct users with different needs and perspectives
- Indirect users affected by the system's operations
- Operators responsible for maintaining the system
- Regulators overseeing compliance
- Communities impacted by the system's effects
- Future generations who inherit the system's consequences

### Feedback Loop Constraints

Agile values feedback, but primarily focuses on feedback that can be quickly obtained and incorporated. This creates blind spots around impacts that emerge gradually, impacting parties not included in feedback loops, or manifesting only at scale or over time.

### Skill and Power Imbalances

Where Agile methodologies often struggle with the uneven distribution of skills, experience, and organizational influence, AD4S directly addresses these imbalances through structured knowledge capture and transparent decision frameworks. The AD4S Ledger transforms team dynamics by making implicit knowledge explicit and contextual, allowing contribution based on insight rather than authority or seniority alone.

By documenting decision contexts, constraints, and alternatives considered, the framework creates a mechanism for meaningful participation regardless of hierarchical position. Junior team members can contribute unique perspectives by referencing captured patterns, while experienced practitioners' wisdom becomes accessible beyond their immediate sphere of influence. This democratization of knowledge doesn't erase skill differences, it leverages them as complementary strengths while preventing them from becoming barriers to sound decision-making.

The framework's emphasis on temporal knowledge graphs further mitigates the impact of inevitable team transitions, ensuring that new team members can easily fill critical gaps in understanding. This approach builds organizational resilience to help everyone "level up" when confronted with a new sub-domain.

## Being Reactive is Not Enough

The Reactive Manifesto makes progress over traditional Agile patterns and practices but still suffers from a form of navel-gazing. Its self-concern imbues an unhealthy projection onto a system's users which in effect is an abdication of responsibility.

It naively creates a tautological loop where it only responds to directed input, and fails to take any notice of larger contextual boundaries in which the system *should* (and in certain legal contexts, must) operate. This includes governance and compliance, privacy, ethics, accessibility and sustainability.

The Reactive approach assumes there will be no contention between competing interests of users (and system managers) and therefore makes no attempt to be the arbiter of where and how certain compromises are to be made. It also assumes there's no potential for misuse or abuse, which is a very dangerous assumption. What if business managers or marketing teams ask engineers to change the system to behave in ways that are illegal or unethical? The Reactive approach has a tacit assumption that if constituencies don't specifically *ask* for these things to be considered, there's no need to address broader systemic concerns.

These blind spots, whether through naivete or by design, are a huge reputational, legal and ultimately business risk that are too important to be left to the whims of individual curators.

## Toward an Outward-Focused Approach

AD4S proposes a fundamental shift from the inward focus of traditional methodologies to an outward focus that acknowledges software's role in complex social, economic, and technological ecosystems. This shift requires:

### Systems Thinking

Recognizing that software exists within larger systems and influences those systems in complex ways that simple cause-and-effect thinking cannot capture.

### Multi-stakeholder Perspective

Explicitly identifying and considering the needs, rights, and interests of all parties affected by the system, not just its direct users or customers.

### Temporal Expansion

Considering impacts across different time horizons, from immediate effects to long-term consequences and legacy concerns.

### Ethical Framing

Incorporating ethical considerations as fundamental design constraints rather than optional considerations or afterthoughts.

### Adaptability Over Dogma

Emphasizing the ability to adapt to changing circumstances rather than rigid adherence to methodological orthodoxy.

## Conclusion: Beyond Navel-gazing

The limitations of traditional SDLC approaches don't negate their value or suggest they should be abandoned. Rather, AD4S proposes plugging into these methodologies with broader perspectives and concerns that address their blind spots.

By recognizing the inward focus that characterizes many development methodologies and deliberately expanding our view to include wider contexts and longer time horizons, we can create systems that not only meet immediate needs but also function responsibly within their larger ecosystems. This outward focus represents a necessary evolution in how we approach software development in an age where digital systems increasingly mediate critical aspects of human experience.

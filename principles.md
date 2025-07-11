## 核心理念

* 质量是第一位的。
* 在保证质量的前提下，才可以追求性能和功能。
* 如果性能上的改进会导致质量的下降，那就不值得做。
* 质量不只是稳定性和可用性，也包括代码的质量。代码劣质，就是质量劣质。
* 质量和速度并不对立，高质量系统可以有更高效率的产出，而不需要浪费时间和人力在还清技术债务上。
* 靠拼人力得来的速度，是用技术债务换来的，迟早得还，速度会被债务拖慢。
* 靠高质量的设计和实现，中长期来讲，技术债务更少，速度可以更快。

## 设计与架构

* 设计应由一两个人做出，以保证概念的完整和一致。
* 设计的粒度应该适当，既不过于粗略，也不过于细化，避免过多限制实现的方式。
* 如果时间精力不够，可以将设计工作委托他人。但不可以因为不懂而委托他人。
* 架构设计，就是设计各个组件之间的接口。从大组件到小组件，都应该先定义接口，再实现。
* 接口应有明确且简洁的语义。如 Unix 哲学所说，"do one thing and do it well"
* 如果现有接口语义不符合需要，就重新定义，而不是打补丁。通过合并和拆分等方式，使新的语义仍然明确且简洁。
* 接口的实现可以是多线程、分布式的，但接口的定义和语义，不应该涉及这些概念，以降低复杂度。
* 接口的调用方不需要关心具体实现是否用到了分布式，只需要关心语义是否正确。
* 接口的定义和语义，应尽量减少对具体实现的假定，以免限制实现的方式，也更容易在测试时注入实现。
* 命名必须使用完整单词，避免阅读代码时无谓的意义猜测或者转换。
* 简洁是相对的，当前认为简洁的设计，可能仍然可以改进，所以需要不断重构。
* 因为接口会有合并和拆分的过程，实现也同样会有合并和拆分，所以“可组合性”是重要的。
* 可组合性更强，合并和拆分就更容易。
* 接口语义不明，语义太多，就难以拆散和组合，就是重构的阻碍。
* 避免在需求不够清晰时过度设计，因为设计还可能迭代多次，所以没必要过于细化。
* 不断重构，软件才能渐趋完美。没有任何设计是从一开始就完美的，所以重构理应是预期中的过程。
* 没有设计，实现就会混乱，难以被所有人理解，质量就会低下。

## 开发流程

* 尽早实现原型并开始演化，避免过早过度设计。
* 软件开发包括设计、实现、重构、测试、优化、除错等相互关联的过程。
* 最重要的是设计。实现和重构，都应该多次进行，让设计不断进化，趋于最佳。
* 一次改动（例如一个拉取请求）应尽可能只做一件事，好处包括：容易调试除错、容易测量影响、需要回滚时影响更小、更容易让成员评审等。

## 质量与测试

* 在设计、实现、重构、优化、部署等过程里，错漏发现得越早，就越容易修复。
* 最好的除错手段，就是不让错误发生。设计和实现越好，错漏就越难以藏身。
* 设计混乱，出现问题不重新设计，只是到处打补丁，就是藏污纳垢的系统。
* 测试贯穿于所有过程，不可缺少。
* 测试可以保证正确性，是重构过程的基石。良好而完备的测试，可以为重构过程带来信心。
* 测试应该有大粒度的，也要有小粒度的。不同粒度的测试，可以暴露不同粒度的错漏。
* 测试应该容易写，应该允许方便地切入系统某一部分做测试。
* 接口明确且简洁，就更容易针对测试需要的场景，使用模拟的实现，更具“可测试性”。
* 任何错漏，都应该用单元测试复现，再修正，而不是手工复现。这样可以保证，错漏修正之后，测试可以一直自动跑，保证以后不会再有同样的错漏。
* 如果难以用单元测试的方式复现错漏，那说明整个架构有问题，应该消除一切阻碍自动化单元测试的因素。
* 测试应该尽可能快速，修正错漏或者优化时，可以得到快速的反馈，提高效率。测试也会一直被自动执行很多次，所以跑得越快越好。
* 尽可能杜绝手工测试。正确性测试和性能测试，应该全部程序化，使不同人在不同环境，都能方便地重复地进行。
* 内部人员在报告错漏时，应提供程序化的复现方式。如果难以做到程序化，就先重构系统，使其容易做到。
* 除错过程里，也可能发现设计中的问题，应该侧重于修正设计问题，而不是给实现打补丁。

## 性能优化

* 在设计相对稳定之后，才开始优化实现的性能。
* 优化应该基于量化指标，而不是直觉。
* 指标测量应明确使用的工具和过程，确保排除人和环境的影响。
* 测量组件或者代码也应经过测试过程，以避免错误。
* 可以引入多套测量，并交叉验证，以避免错误。
* 错误的测量比没有测量更糟糕，基于错误测量的决策，会造成相当大的时间或人力浪费。
* 不应过早优化细节，应该设计相对稳定，正确性得到保证之后，再优化细节。

## 环境与工具

* 开发或者生产环境，应能方便地搭建。搭建过程应尽量减少手工输入，避免出错。
* 开发或者生产环境，应能方便地创建快照，包括数据快照和程序快照。
* 每个开发者应有单独的开发环境，禁止共用开发环境，禁止多人、同步、手工复现等调试方式。
* 在开发环境复现生产环境的错漏，应该尽可能方便。如果不方便，就不断重构直到可以方便重现。
* 用代码管理所有的环境配置，纳入版本管理。
* 使用自动化工具，结合人工智能，强化原则的实施。
	* 代码质量评估
	* 设计质量评估
	* 代码变更预评审
	* 生成及运行测试
	* 性能测量
	* 系统瓶颈分析
	* 概括成员行为及表现

## 可观测性与接口

* 系统里正在发生的、发生过的、将要发生的事情，应能方便地获知。
* 文本、图形、查询语言等界面，都应该尽量提供，而不是局限于一种。
* 不同界面应使用同样的数据源，避免不一致。

## 组织与文化

* 组织的成员，应有共同的理念和追求。注重质量而不是数量，推崇脑力而不是体力，讲究平等而不是倾轧，开放而不混乱，守纪而不迂腐，敢于直言和面对诤言，拥抱变化而不忘记初衷。
* 避免固化的层级式的组织。针对具体的任务或者关注点，设立小队。
* 一位成员可以属于不同的小队。队内的分工应明确。
* 尽量使用人工智能来替代中层角色，以避免这些问题：信息传递失真、决策缓慢、限制成员自主性和创造力等。
* 人工智能做得好的事情，就让人工智能来做。
* 避免使用机械化的效能评价指标，如代码量之类。隐藏评价标准，以避免针对性的优化和博弈。
* 组织的理念不一定在任何情况下都可以践行，如果不得不做有违理念的事情，需要做好隔离和切割，尽力降低对组织和理念的影响。
* 对于新加入的成员，需要有良好的引导和培训，帮助他们理解组织的理念，以及合适的实践方式。
* 尊重每一位成员，维护成员的动力和热情，维护积极、有趣、安全的工作环境。
* 沟通应该尽量高效。设计良好的系统和组织，容易被理解和运作，需要的沟通就少。
* 沟通应该异步。同步的会议会无谓消耗所有人的时间和精力，应该在有限的情况下使用：紧急问题处理、复杂问题同步等。
* 沟通应该有书面记录和可搜索，方便将来的使用，及人工智能的处理。
* 沟通应该多提供事实，避免过早判断，避免A-B问题。
* 沟通应使用共同认可的概念集，避免使用不同的词汇表，导致理解偏差。
* 如果项目参与者之间存在多套的术语系统，应尽快纠正为统一的一套。
* 进度的跟踪，优先使用人工智能实现。将所有设计、代码、及其他活动记录作为输入，得出当前进度。
* 不是所有人都会因践行原则而受益。有些角色的利益关系，天然和原则冲突，所以应尽量减少组织内这类角色。
	* 例如有些角色的目标只是短期的表面的进度和效果，并不关心长期的质量或者技术债务，所以不可以让这类角色主导工作。
	* 或者将成员与职责分离，让成员动态地轮流担任这类职责，使利益一体化，减少冲突。

## 原则的演进

* 上述理念并不是真理，需要持续的改进。尤其需要关注这些方面：
	* 在实际环境下难以实践
	* 有更好的替代理念
	* 因为预设条件变化而变得过时
	* 容易表面上被遵循，但实际有悖根本原则，沦为教条


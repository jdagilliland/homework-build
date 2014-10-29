import os

# Use python to build a plot
plotbuild = Builder(
    action='python $SOURCE $TARGET',
    suffix='.png', src_suffix='.py',
    )

# Use python to build a table
tablebuild = Builder(
    action='python $SOURCE $TARGET',
    suffix='.csv', src_suffix='.py',
    )

# Use pygments to build a source code listing
pygbuild = Builder(
    action='pygmentize -O linenos=True,linenostep=5 \
            -o $TARGET $SOURCE',
        )

env=Environment(BUILDERS = {
    'Plot': plotbuild,
    'Table': tablebuild,
    'Pyg': pygbuild,
    })

pygheaders = env.Command('build/pygstyle.tex','pygstyle.sh',
    'sh $SOURCE > $TARGET')

# Look in standard directory ~/texmf for .sty files
env['ENV']['TEXMFHOME'] = os.path.join(os.environ['HOME'],'texmf')
ps00 = env.PDF(target='ps00.pdf', source='ps00.tex')
prob2_plot = env.Plot(target='build/cobweb.png',
        source='src/book_prob02.py')
Depends(prob2_plot, ['src/cobweb.py'])
exer1_src = env.Pyg(
        target='build/code_sample.tex',
        source='src/code_sample.m',
        )
Depends(ps00, [
    prob2_plot,
    exer1_src,
    ])

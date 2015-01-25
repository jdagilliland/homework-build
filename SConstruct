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
    },
    TARFLAGS = '-czh',
    )

pygheaders = env.Command('build/pygstyle.tex','pygstyle.sh',
    'sh $SOURCE > $TARGET')

# Look in standard directory ~/texmf for .sty files
env['ENV']['TEXMFHOME'] = os.path.join(os.environ['HOME'],'texmf')

# This needs to change with the chosen homework name
main_base = 'ps00'

# Build the main PDF
main_pdfbuild = env.PDF(target=main_base+'.pdf', source=main_base+'.tex')

# Build plot with a dependency on a separate module
prob2_plot = env.Plot(target='build/cobweb.png',
        source='src/book_prob02.py')
Depends(prob2_plot, ['src/cobweb.py'])

# Build the code listing
def texname(matname):
    base = matname.rpartition('.')[0]
    return base + '.tex'
lst_mat_name = [fname for fname in os.listdir('src')
        if fname[-2:] == '.m']
lst_mat_src = [env.Pyg(
    target=os.path.join('build/', texname(matname)),
    source=os.path.join('src/', matname),
    ) for matname in lst_mat_name]

# Build the tar archive
tarf = env.Tar(main_base+'.tar.gz', [
    'build/',
    'src/',
    'jdaghw.sty',
    main_base+'.tex',
    'pygstyle.sh',
    'SConstruct',
    ])
Depends(main_pdfbuild, [
    prob2_plot,
    lst_mat_src,
    ])
Default(main_pdfbuild)

# SportsPulse
A sports website that gives authentic news update on sports and other related activities.
import React, { useState, useEffect } from 'react';
import { 
  Menu, 
  X, 
  Moon, 
  Sun, 
  Newspaper, 
  ArrowRightLeft, 
  Activity, 
  Trophy, 
  Users, 
  Plus, 
  User, 
  Share2, 
  MessageSquare,
  ChevronRight,
  Clock,
  MapPin
} from 'lucide-react';

const App = () => {
  const [darkMode, setDarkMode] = useState(false);
  const [sidebarOpen, setSidebarOpen] = useState(false);
  const [activeTab, setActiveTab] = useState('news');
  const [showModal, setShowModal] = useState(false);

  // Mock Data State
  const [posts, setPosts] = useState([
    {
      id: 1,
      type: 'news',
      title: "Championship Final Date Set",
      content: "The league has officially announced the dates for the upcoming grand final at the Blue Arena. Tickets go on sale Friday.",
      time: "2h ago",
      author: "Admin",
      image: "https://images.unsplash.com/photo-1504450758481-7338eba7524a?auto=format&fit=crop&q=80&w=500"
    },
    {
      id: 2,
      type: 'transfer',
      title: "Star Striker to Blues FC",
      content: "Sources confirm the $50M deal is nearly complete. Medicals are scheduled for tomorrow morning.",
      time: "4h ago",
      author: "Transfer Desk",
      image: "https://images.unsplash.com/photo-1522778119026-d647f0565c71?auto=format&fit=crop&q=80&w=500"
    },
    {
      id: 3,
      type: 'live',
      match: "Blues FC vs. Red United",
      score: "2 - 1",
      status: "78'",
      details: "Goal! Johnson scores a header from the corner kick.",
      league: "Premier League"
    },
    {
      id: 4,
      type: 'results',
      match: "City Warriors vs. Northern Lights",
      score: "0 - 3",
      status: "FT",
      date: "Yesterday",
      league: "Cup Semi-Final"
    },
    {
      id: 5,
      type: 'team',
      title: "Training Camp Update",
      content: "The squad has arrived in Spain for the mid-season training camp. All players are fit and available.",
      time: "1d ago",
      author: "Team Physio"
    }
  ]);

  // Handle "Uploading" new content
  const [newPost, setNewPost] = useState({ title: '', content: '', type: 'news' });

  const handleUpload = (e) => {
    e.preventDefault();
    const post = {
      id: Date.now(),
      type: newPost.type,
      title: newPost.title,
      content: newPost.content,
      time: "Just now",
      author: "You",
      match: newPost.title, 
      score: "0 - 0",
      status: "Live",
      league: "Friendly Match"
    };
    setPosts([post, ...posts]);
    setShowModal(false);
    setNewPost({ title: '', content: '', type: 'news' });
    setActiveTab(newPost.type);
  };

  const toggleDarkMode = () => setDarkMode(!darkMode);
  
  const categories = [
    { id: 'news', label: 'News', icon: Newspaper },
    { id: 'transfer', label: 'Transfers', icon: ArrowRightLeft },
    { id: 'live', label: 'Live Scores', icon: Activity },
    { id: 'results', label: 'Results', icon: Trophy },
    { id: 'team', label: 'Team Updates', icon: Users },
  ];

  return (
    <div className={`min-h-screen transition-colors duration-300 font-sans ${darkMode ? 'dark bg-slate-900 text-white' : 'bg-slate-50 text-slate-900'}`}>
      
      {/* --- Header --- */}
      <header className={`fixed top-0 w-full z-40 transition-colors duration-300 border-b ${darkMode ? 'bg-slate-900/95 border-slate-700 backdrop-blur-md' : 'bg-white/95 border-slate-200 backdrop-blur-md'}`}>
        <div className="flex items-center justify-between px-4 h-16 max-w-5xl mx-auto">
          
          {/* Menu Button (Top Left) */}
          <button 
            onClick={() => setSidebarOpen(true)}
            className={`p-2 rounded-lg transition-colors focus:outline-none focus:ring-2 focus:ring-blue-500 ${darkMode ? 'hover:bg-slate-800 text-blue-400' : 'hover:bg-blue-50 text-blue-600'}`}
            aria-label="Open Menu"
          >
            <Menu size={28} strokeWidth={2.5} />
          </button>

          {/* Logo */}
          <h1 className="text-2xl font-black tracking-tighter text-blue-600 italic select-none">
            SPORTS<span className={darkMode ? 'text-white' : 'text-slate-800'}>PULSE</span>
          </h1>

          {/* Dark Mode Toggle */}
          <button 
            onClick={toggleDarkMode}
            className={`p-2 rounded-full transition-all duration-300 focus:outline-none focus:ring-2 focus:ring-offset-2 ${darkMode ? 'bg-slate-800 text-yellow-400 hover:bg-slate-700 focus:ring-slate-500' : 'bg-slate-100 text-slate-600 hover:bg-slate-200 focus:ring-blue-400'}`}
            aria-label="Toggle Dark Mode"
          >
            {darkMode ? <Sun size={20} /> : <Moon size={20} />}
          </button>
        </div>
      </header>

      {/* --- Sidebar Navigation --- */}
      <div className={`fixed inset-0 z-50 transition-opacity duration-300 ${sidebarOpen ? 'opacity-100' : 'opacity-0 pointer-events-none'}`}>
        {/* Overlay */}
        <div 
          className="absolute inset-0 bg-black/60 backdrop-blur-sm"
          onClick={() => setSidebarOpen(false)}
        />
        
        {/* Drawer */}
        <aside 
          className={`absolute top-0 left-0 h-full w-80 shadow-2xl transform transition-transform duration-300 ease-out flex flex-col ${darkMode ? 'bg-slate-800 text-white' : 'bg-white text-slate-900'} ${sidebarOpen ? 'translate-x-0' : '-translate-x-full'}`}
        >
          {/* Profile Section inside Sidebar (Top Left context) */}
          <div className="p-6 border-b border-white/10 flex flex-col items-center text-center bg-blue-600 relative overflow-hidden">
             {/* Decorative circles */}
             <div className="absolute top-[-20px] left-[-20px] w-24 h-24 bg-white/10 rounded-full"></div>
             <div className="absolute bottom-[-10px] right-[-10px] w-16 h-16 bg-white/10 rounded-full"></div>

            <button 
              onClick={() => setSidebarOpen(false)}
              className="absolute top-4 right-4 text-white/80 hover:text-white p-1 rounded-full hover:bg-white/20 transition-colors"
            >
              <X size={24} />
            </button>

            <div className="relative mb-3 mt-4">
              <div className="w-20 h-20 rounded-full bg-white flex items-center justify-center text-blue-600 shadow-xl border-4 border-white/30">
                <User size={40} />
              </div>
              <div className="absolute bottom-1 right-0 w-5 h-5 bg-green-400 rounded-full border-2 border-blue-600"></div>
            </div>
            <h2 className="text-xl font-bold text-white tracking-tight">Admin User</h2>
            <p className="text-blue-100 text-sm font-medium">Head Editor</p>
          </div>

          {/* Navigation Links */}
          <nav className="flex-1 overflow-y-auto py-6 px-3 space-y-2">
            {categories.map((cat) => (
              <button
                key={cat.id}
                onClick={() => {
                  setActiveTab(cat.id);
                  setSidebarOpen(false);
                }}
                className={`w-full flex items-center space-x-4 px-4 py-3 rounded-xl transition-all duration-200 font-medium group ${
                  activeTab === cat.id 
                    ? 'bg-blue-600 text-white shadow-lg shadow-blue-600/30' 
                    : darkMode 
                      ? 'text-slate-400 hover:bg-slate-700 hover:text-white' 
                      : 'text-slate-600 hover:bg-blue-50 hover:text-blue-600'
                }`}
              >
                <cat.icon size={20} className={`transition-transform duration-200 ${activeTab === cat.id ? 'scale-110' : 'group-hover:scale-110'}`} />
                <span>{cat.label}</span>
                {activeTab === cat.id && <ChevronRight size={16} className="ml-auto opacity-70" />}
              </button>
            ))}
          </nav>

          <div className="p-6 border-t border-gray-200 dark:border-slate-700 text-xs text-center opacity-40">
            <p className="font-semibold mb-1">SportsPulse v1.0</p>
            <p>Developed for Sports Fans</p>
          </div>
        </aside>
      </div>

      {/* --- Main Content --- */}
      <main className="pt-20 pb-24 px-4 max-w-2xl mx-auto min-h-screen">
        
        {/* Section Header */}
        <div className="mb-6 mt-4 flex items-center justify-between sticky top-16 z-30 py-2 transition-colors">
          <h2 className="text-2xl font-bold flex items-center capitalize tracking-tight">
            {activeTab === 'live' ? 'Live Scores' : activeTab}
          </h2>
          <span className={`px-3 py-1 text-xs font-bold rounded-full uppercase tracking-wide flex items-center gap-1 ${darkMode ? 'bg-blue-900/50 text-blue-300' : 'bg-blue-100 text-blue-700'}`}>
            <Clock size={12} /> Latest
          </span>
        </div>

        {/* Content Feed */}
        <div className="space-y-5">
          {posts.filter(p => p.type === activeTab).length === 0 ? (
            <div className="text-center py-20 opacity-50 flex flex-col items-center">
              <div className={`p-6 rounded-full mb-4 ${darkMode ? 'bg-slate-800' : 'bg-slate-200'}`}>
                 <Newspaper size={48} className="opacity-50"/>
              </div>
              <p className="text-lg font-medium">No updates available</p>
              <p className="text-sm">Be the first to upload content here.</p>
            </div>
          ) : (
            posts.filter(p => p.type === activeTab).map((post) => (
              <div 
                key={post.id} 
                className={`group rounded-2xl overflow-hidden shadow-sm hover:shadow-lg transition-all duration-300 border ${darkMode ? 'bg-slate-800 border-slate-700 hover:border-slate-600' : 'bg-white border-slate-100 hover:border-blue-100'}`}
              >
                {/* Image for News/Transfer */}
                {(post.type === 'news' || post.type === 'transfer') && post.image && (
                  <div className="h-48 w-full overflow-hidden relative">
                     <img src={post.image} alt={post.title} className="w-full h-full object-cover transform group-hover:scale-105 transition-transform duration-500" />
                     <div className={`absolute top-3 left-3 text-[10px] font-black tracking-widest px-2 py-1 rounded uppercase shadow-sm ${post.type === 'transfer' ? 'bg-yellow-400 text-black' : 'bg-blue-600 text-white'}`}>
                       {post.type}
                     </div>
                  </div>
                )}

                {/* Score Card Design for Live/Results */}
                {(post.type === 'live' || post.type === 'results') && (
                  <div className="p-6 bg-gradient-to-br from-blue-600 to-blue-800 text-white relative overflow-hidden">
                    {/* Background Pattern */}
                    <div className="absolute inset-0 opacity-10 bg-[radial-gradient(circle_at_center,_var(--tw-gradient-stops))] from-white via-transparent to-transparent"></div>
                    
                    <div className="relative z-10 text-center">
                      <div className="flex items-center justify-center gap-2 text-xs font-bold opacity-80 mb-6 uppercase tracking-widest">
                        <Trophy size={12} /> {post.league}
                      </div>
                      
                      <div className="flex items-center justify-between text-lg font-bold mb-4">
                        <span className="w-2/5 text-right leading-tight">{post.match.split('vs.')[0]}</span>
                        
                        <div className="flex flex-col items-center px-2">
                           <span className={`px-3 py-1 rounded-md text-2xl font-black min-w-[80px] ${post.type === 'live' ? 'bg-red-500 shadow-red-900/50 shadow-lg' : 'bg-white/20'}`}>
                             {post.score}
                           </span>
                           <span className="mt-1 text-[10px] font-mono bg-black/30 px-2 rounded">
                             {post.status}
                           </span>
                        </div>

                        <span className="w-2/5 text-left leading-tight">{post.match.split('vs.')[1]}</span>
                      </div>
                      
                      {post.details && (
                        <div className="mt-4 pt-4 border-t border-white/10 text-sm opacity-90 italic flex items-center justify-center gap-2">
                          <Activity size={14} />
                          "{post.details}"
                        </div>
                      )}
                    </div>
                  </div>
                )}

                {/* Regular Content Body */}
                {(post.type !== 'live' && post.type !== 'results') && (
                  <div className="p-5">
                    <h3 className="text-xl font-bold mb-2 leading-tight group-hover:text-blue-500 transition-colors">
                      {post.title}
                    </h3>
                    <p className={`mb-4 text-sm leading-relaxed ${darkMode ? 'text-slate-400' : 'text-slate-600'}`}>
                      {post.content}
                    </p>
                    <div className="flex items-center justify-between text-xs opacity-60 font-medium">
                      <span className="flex items-center"><User size={12} className="mr-1"/> {post.author}</span>
                      <span className="flex items-center"><Clock size={12} className="mr-1"/> {post.time}</span>
                    </div>
                  </div>
                )}

                {/* Interaction Footer */}
                <div className={`px-5 py-3 border-t flex items-center justify-between text-sm ${darkMode ? 'border-slate-700 bg-slate-800/50' : 'border-slate-50 bg-slate-50'}`}>
                   <button className="flex items-center gap-2 hover:text-blue-500 transition-colors">
                     <Share2 size={16} /> <span className="hidden sm:inline">Share</span>
                   </button>
                   <button className="flex items-center gap-2 hover:text-blue-500 transition-colors">
                     <MessageSquare size={16} /> <span className="hidden sm:inline">Comment</span>
                   </button>
                </div>
              </div>
            ))
          )}
        </div>
      </main>

      {/* --- Floating Action Button (Upload) --- */}
      <button
        onClick={() => setShowModal(true)}
        className="fixed bottom-6 right-6 w-14 h-14 bg-blue-600 hover:bg-blue-500 text-white rounded-full shadow-lg shadow-blue-600/40 flex items-center justify-center transition-all hover:scale-110 active:scale-95 z-40 group"
        aria-label="Upload Content"
      >
        <Plus size={28} className="transition-transform group-hover:rotate-90" />
      </button>

      {/* --- Upload Modal --- */}
      {showModal && (
        <div className="fixed inset-0 z-50 flex items-end sm:items-center justify-center p-4 sm:p-6">
          <div className="absolute inset-0 bg-black/70 backdrop-blur-sm transition-opacity" onClick={() => setShowModal(false)} />
          
          <div className={`relative w-full max-w-lg rounded-2xl shadow-2xl p-6 transform transition-all scale-100 ${darkMode ? 'bg-slate-800' : 'bg-white'}`}>
            <div className="flex justify-between items-center mb-6">
              <h3 className="text-xl font-bold">New Post</h3>
              <button 
                onClick={() => setShowModal(false)}
                className="p-1 rounded-full hover:bg-black/10 transition-colors"
              >
                <X size={20} />
              </button>
            </div>
            
            <form onSubmit={handleUpload} className="space-y-5">
              <div>
                <label className={`block text-xs font-bold uppercase tracking-wider mb-2 ${darkMode ? 'text-slate-400' : 'text-slate-500'}`}>Category</label>
                <div className="grid grid-cols-2 gap-2">
                   {categories.slice(0, 4).map(cat => (
                     <button
                       key={cat.id}
                       type="button"
                       onClick={() => setNewPost({...newPost, type: cat.id})}
                       className={`p-2 rounded-lg border text-sm flex items-center justify-center gap-2 transition-all ${newPost.type === cat.id ? 'bg-blue-600 text-white border-blue-600' : darkMode ? 'border-slate-600 hover:bg-slate-700' : 'border-slate-200 hover:bg-slate-50'}`}
                     >
                       <cat.icon size={16} /> {cat.label}
                     </button>
                   ))}
                </div>
              </div>

              <div>
                <label className={`block text-xs font-bold uppercase tracking-wider mb-2 ${darkMode ? 'text-slate-400' : 'text-slate-500'}`}>
                  {newPost.type === 'live' || newPost.type === 'results' ? 'Matchup (e.g. Home vs Away)' : 'Title'}
                </label>
                <input 
                  required
                  type="text" 
                  className={`w-full p-3 rounded-xl border outline-none focus:ring-2 focus:ring-blue-500 transition-all ${darkMode ? 'bg-slate-900 border-slate-700 text-white placeholder-slate-500' : 'bg-slate-50 border-slate-200 text-slate-900'}`}
                  placeholder={newPost.type === 'news' ? "e.g. Major Signing Announced" : "e.g. Blues vs Reds"}
                  value={newPost.title}
                  onChange={(e) => setNewPost({...newPost, title: e.target.value})}
                />
              </div>

              <div>
                <label className={`block text-xs font-bold uppercase tracking-wider mb-2 ${darkMode ? 'text-slate-400' : 'text-slate-500'}`}>Content / Details</label>
                <textarea 
                  required
                  rows="3"
                  className={`w-full p-3 rounded-xl border outline-none focus:ring-2 focus:ring-blue-500 transition-all ${darkMode ? 'bg-slate-900 border-slate-700 text-white placeholder-slate-500' : 'bg-slate-50 border-slate-200 text-slate-900'}`}
                  placeholder="Enter the main details here..."
                  value={newPost.content}
                  onChange={(e) => setNewPost({...newPost, content: e.target.value})}
                />
              </div>

              <button 
                type="submit"
                className="w-full py-4 bg-blue-600 hover:bg-blue-500 text-white font-bold rounded-xl transition-all transform active:scale-95 shadow-lg shadow-blue-600/30 flex items-center justify-center gap-2"
              >
                <span>Publish Update</span> <ChevronRight size={18} />
              </button>
            </form>
          </div>
        </div>
      )}

    </div>
  );
};

export default App;


